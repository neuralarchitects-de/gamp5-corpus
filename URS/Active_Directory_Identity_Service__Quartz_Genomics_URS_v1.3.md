---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; Wave 3 Chunk J expanded 2026-05-12 (T3 catch-up: JML lifecycle, PAM/JIT, FIDO2/phishing-resistant MFA, Kerberos hygiene, hybrid Entra ID, NIS2, ISO/IEC 27001:2022, NIST SP 800-63B alignment, forest-recovery + tier-0 hardening, per-ID Part 11 sub-section bindings)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed., 2022) Cat 3 conventions for non-configured infrastructure software"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11 §§ 4, 7, 9, 12"
  - "PIC/S PI 041"
  - "ISO/IEC 27001:2022 (Annex A controls A.5, A.8, A.9, A.12, A.16, A.17)"
  - "NIST SP 800-63B Digital Identity Guidelines (Authenticator + Lifecycle)"
  - "NIST SP 800-53 Rev. 5 (AC, AU, IA, SC families)"
  - "NIS2 Directive (EU) 2022/2555 (essential entities; incident reporting; supply-chain security)"
  - "GDPR Reg. (EU) 2016/679 Art. 32 (security of processing)"
  - "ISPE GAMP GPG IT Infrastructure Control and Compliance"
  - "BSI IT-Grundschutz Kompendium ORP.4 (Identitäts- und Berechtigungsmanagement)"
  - "Microsoft — Securing Active Directory (Tiered Access Model + Enterprise Access Model)"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Active Directory Identity Service — Microsoft Windows Server 2022 AD DS + Microsoft Entra ID Connect + ADCS PKI

**Document Number:** QTZ-URS-AD-001 | **Version:** 1.1 | **Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Quartz Genomics Ltd, Global IT Identity Operations, Cambridge, United Kingdom *(fictional)* — with EU primary identity hub at the Munich (DE) data centre and DR hub at the Basel (CH) co-location
**System Owner:** Identity Services Lead
**Process Owner:** Head of IT
**System Class (GAMP 5, 2nd ed.):** Category 3 — Non-Configured Product (commercial directory software deployed to Microsoft's reference architecture; site does not author code or scripts that materially affect identity logic beyond standard configuration)
**Project Mode:** Configuration project on non-configurable instrument / appliance **Microsoft Windows Server 2022 AD DS + Microsoft Entra ID Connect + ADCS PKI** (GAMP 5 Category 3 — Non-Configurable COTS).
**Regulatory Scope:** 21 CFR Part 11 §§ .10(a/b/c/d/e/g/k), .30, .100, .200, .300; EU GMP Annex 11 §§ 4, 7, 9, 12; PIC/S PI 041; ISO/IEC 27001:2022 (Annex A.5/A.8/A.9/A.12/A.16/A.17); NIST SP 800-63B; NIS2 Directive (EU) 2022/2555; GDPR Art. 32; BSI IT-Grundschutz ORP.4

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Identity Services Lead) | _____________ | _____________ | _____ |
| Reviewer (Information Security Officer / CISO delegate) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Data Protection Officer — GDPR Art. 32 scope) | _____________ | _____________ | _____ |
| Approver (Head of IT) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |
| Approver (CISO) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. 11 §5 subsections, ~30 requirements. |
| 1.1 | 2026-05-12 | (synthetic) | **Authored to Tier T3** (large enterprise identity platform — 100-150 req target; spans JML lifecycle + AuthN + AuthZ + PAM + Kerberos hygiene + hybrid Entra ID + DR/BCP + cybersecurity + audit/SIEM + NIS2 incident reporting + per-Part 11 sub-section bindings). Adds 16 §5 subsections; per-ID Part 11 sub-section citations; FIDO2 phishing-resistant MFA; gMSA / vault-managed service accounts; JIT elevation; tier-0 isolation; conditional access; ISO 27001:2022 controls. |

## Definitions

| Term | Definition |
|---|---|
| AD DS | Active Directory Domain Services (on-prem) |
| Forest / Domain | AD logical containers; Quartz uses one forest with one production domain (`quartz.local`) and one isolated tier-0 administrative forest (`admin.quartz.local`, RED forest pattern) |
| DC | Domain Controller |
| RODC | Read-Only Domain Controller (DMZ + branch placements) |
| Entra ID | Microsoft cloud identity (formerly Azure AD); Entra ID Connect synchronises on-prem AD with Entra ID; Entra Connect Cloud Sync used for branch tenants |
| Conditional Access (CA) | Entra ID policy engine evaluating signals (user, device, location, risk) at sign-in |
| MFA | Multi-Factor Authentication |
| FIDO2 | Phishing-resistant authenticator standard (WebAuthn + CTAP2); hardware security key |
| TOTP | Time-based One-Time Password (RFC 6238) — not phishing-resistant; used only for non-privileged remediation fallback |
| gMSA | Group Managed Service Account (Windows-native; password automatically rotated by AD) |
| PAW | Privileged Access Workstation (hardened tier-0 workstation) |
| PAM | Privileged Access Management (CyberArk PAM / Entra PIM) |
| JIT | Just-In-Time elevation (time-bounded membership in privileged groups) |
| Tier 0 / 1 / 2 | Microsoft Enterprise Access Model (Tier 0 = identity control plane; Tier 1 = enterprise servers; Tier 2 = user workstations) |
| RBAC / ABAC | Role-Based / Attribute-Based Access Control |
| SCIM | System for Cross-domain Identity Management (RFC 7644) provisioning protocol |
| SoD | Segregation of Duties |
| ADCS | Active Directory Certificate Services (PKI) |
| HSM | Hardware Security Module |
| KDC | Key Distribution Center (Kerberos) |
| SIEM | Security Information and Event Management (Splunk Enterprise Security) |
| SOC | Security Operations Centre |
| NIS2 | EU Directive 2022/2555 — Network and Information Security 2 |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| RTO / RPO | Recovery Time / Point Objective |
| HRIS | Human Resources Information System (Workday) — authoritative source for joiner / mover / leaver |

## 1. Purpose

This URS defines requirements for the Active Directory identity service that authenticates and authorises users across all GxP applications and infrastructure at Quartz Genomics. Because every GxP application federates to AD (directly via Kerberos / LDAPS, or via Entra ID using SAML 2.0 / OIDC), AD is itself in GxP scope as a Cat-3 critical infrastructure component. Its compromise would invalidate the unique-user-identity foundation that 21 CFR Part 11 §§ .100, .200 and EU GMP Annex 11 § 12 depend upon. Quartz Genomics is additionally classified as an *essential entity* under NIS2 Directive (EU) 2022/2555 (manufacture of medicinal products, Annex I sector 5) — AD is therefore in scope of the NIS2 cybersecurity and incident-reporting regime in addition to GxP regulation.

## 2. Scope

**In scope:** the AD DS forest (`quartz.local`) with the production domain; one isolated tier-0 administrative forest (`admin.quartz.local`) implementing the Microsoft RED forest pattern; eight geographically distributed domain controllers (3 in Cambridge UK + 2 in München DE + 1 in Singapore + 1 in Boston US + 1 in São Paulo BR), with two of the UK and one of the DE DCs designated as global-catalog + FSMO host pool; two read-only DCs (RODC) in DMZ for branch sites; Entra ID hybrid federation to the tenant `quartzgenomics.onmicrosoft.com` with conditional access, MFA (Authenticator app + FIDO2 hardware keys), and Entra PIM for cloud-side JIT elevation; ADCS two-tier PKI (offline root + two issuing CAs, HSM-protected) issuing user / device / signing / service certificates; group policy infrastructure controlling password policy, screen-lock, removable-media restrictions, Office macro-disable, BitLocker, Defender baseline; the privileged access management platform (CyberArk PAM) gating tier-0 + tier-1 admin sessions with credential vaulting + session recording; the privileged-access workstation (PAW) infrastructure for tier-0 admins; SCIM provisioning to SaaS GxP applications (LMS, eQMS, ePRO portal); the AD-event-forwarding pipeline to the site SIEM (Splunk Enterprise Security) and the SOC.

**Out of scope:** application-level authorization configuration (governed by per-application URS); Entra ID cloud-only features outside the synced-identity scope; Microsoft 365 service-tenant configuration; downstream-application e-signature manifestation (governed by application-level URS, though AD provides the unique-identity foundation per § 11.100); third-party customer-facing portal identity (managed in a separate Entra External ID tenant).

### 2.1 Information Flow Summary

At a high level the data flows are:

1. **HRIS → AD:** the HRIS (Workday) is the authoritative source for joiner / mover / leaver events; the provisioning pipeline consumes Workday events and creates / modifies / disables AD accounts. AD is never a primary record-system for HR data.
2. **AD → Entra ID:** Entra ID Connect synchronises on-prem identities to the cloud tenant; password-hash-sync provides the cloud credential. Tier-0 accounts are excluded from sync.
3. **AD → GxP applications (on-prem):** Kerberos / LDAPS authentication; group-membership-based authorisation.
4. **Entra ID → GxP applications (SaaS):** SAML 2.0 / OIDC + conditional access; SCIM provisioning for lifecycle.
5. **ADCS → AD / Endpoints / Users:** certificate issuance via auto-enrolment templates; CRL / OCSP for revocation.
6. **AD + Entra ID → SIEM (Splunk):** audit-event forwarding for inspection-readiness + security correlation.
7. **CyberArk PAM ↔ AD:** broker for privileged sessions; credential vaulting; session recording; JIT elevation.
8. **Backup System → AD:** nightly system-state backups; periodic restore-validation tests.

## 3. System Description and Intended Use

AD DS is the on-prem identity authority for the Quartz Genomics enterprise. Users authenticate to AD; all GxP applications federate to AD (Kerberos / NTLMv2 / LDAPS) or to Entra ID (SAML 2.0 / OIDC) using identities synced via Entra ID Connect. AD also enforces password policy, account lockout, computer policies (screen lock, removable media, macro disable, BitLocker, Defender baseline), and group memberships that drive role-based access in downstream applications. ADCS issues per-user signing certificates that satisfy the public-key half of certificate-based e-signatures in select GxP applications, and per-device certificates for 802.1X network access control.

The site implements the Microsoft Enterprise Access Model with strict Tier 0 (identity control plane) / Tier 1 (enterprise servers) / Tier 2 (user workstations) isolation. Tier-0 administration runs from a separate administrative forest, with one-way trust + Selective Authentication. Tier-0 admins use only Privileged Access Workstations.

The system is GAMP Cat 3: AD DS, Entra ID, ADCS, and CyberArk are commercial products deployed to vendor reference architecture; Quartz authors no significant custom code. Schema modifications, custom PowerShell automation, and provisioning logic that would materially affect identity decisioning would re-classify those components to Cat 5 and trigger custom-SDLC; none are in production scope today. Configuration items (e.g., GPO content, group naming convention, conditional-access policy rules) are change-controlled at Cat-3 depth via the IT change-management process.

## 4. User Roles

| Role | Permissions | SoD enforcement |
|---|---|---|
| Standard User | Authenticate; access applications per AD-group membership; cannot create / modify groups or other users. | — |
| Application Owner | Request AD-group creation / user assignment via ticketing; cannot self-assign; cannot directly modify AD. | Ticket workflow requires a second approver from QA or business. |
| Service-Desk Operator (Tier 2) | Reset user passwords (per documented procedure); unlock accounts; cannot create / modify AD groups affecting GxP applications; cannot reset privileged accounts. | Privileged-account resets routed to Identity Engineer. |
| GxP Access Approver (App Owner + QA co-sign) | Co-approve user assignment to GxP-application AD groups via ticket workflow. | Two-person rule per access request. |
| Identity Engineer (Tier 1) | Configure AD (DNS, replication, GPO under change control); manage gMSA / service accounts; cannot approve own changes; cannot perform tier-0 actions. | Approval routed to Identity Approver pair. |
| Identity Approver (Identity Services Lead + InfoSec Officer co-sign) | Co-approve identity-infrastructure changes. | Two-person rule per CR. |
| PKI Operator | Operate ADCS issuing CAs (issuance / revocation); cannot modify root CA. | Root-CA operations require key-ceremony quorum. |
| Tier-0 Administrator | Domain Admin / Enterprise Admin / Schema Admin actions; only via PAW; only with JIT activation + break-glass justification + InfoSec witness. | Group memberships empty by default; JIT-only. |
| Tier-0 Break-Glass Account (×2) | Emergency root credentials; safe-stored; physically dual-controlled. | Use triggers automatic SOC alert + post-event review. |
| Auditor / Inspector | Read-only access to AD audit logs, configuration baselines, change records. | — |
| Data Protection Officer (DPO) | Read access to logs for GDPR Art. 32 audit + Art. 33 incident scoping. | — |
| SOC Analyst | Read access to AD events forwarded to SIEM; trigger incident workflow. | — |

**Separation of duties (system-enforced wherever possible, otherwise procedurally + audit-reviewed):**

- Identity Engineer ≠ Approver of own change.
- Service-Desk ≠ GxP Access Approver.
- Tier-0 actions follow JIT activation with InfoSec witness and post-event review.
- PKI root-CA quorum: ≥ 2 of 3 named operators are required to be physically present for any root operation (key ceremony).
- Break-glass accounts: dual physical custody; opening the safe triggers SOC alert; post-use full forensic review within 5 business days.

## 5. User Requirements

Requirements are organised into eighteen subsections covering architecture, identity lifecycle, authentication, authorisation, privileged-access management, service accounts, endpoint configuration, Kerberos hygiene, hybrid cloud, PKI, audit, Part 11 sub-section alignment, cybersecurity / NIS2, backup + DR, performance + availability, monitoring, and training + periodic review. Every requirement is a verifiable `shall`-clause carrying an ID, Priority (H/M/L), and Risk class (R1 immediate-GxP-impacting / R2 indirect / R3 administrative). Where a requirement implements a specific 21 CFR Part 11 sub-section, it is cited explicitly (§ 5.13 consolidates the Part-11 sub-section map).

### 5.1 Forest / Domain Architecture

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ARCH-01 | H | R1 | The system **shall** maintain a single production forest (`quartz.local`) with a single production domain plus an isolated tier-0 administrative forest (`admin.quartz.local`) following the Microsoft RED-forest / Enterprise Access Model with a one-way trust + Selective Authentication. |
| URS-ARCH-02 | H | R1 | The system **shall** operate eight domain controllers across five geographies; replication topology **shall** be designed for resilience to any single-site failure with no GxP-application outage. |
| URS-ARCH-03 | H | R1 | Forest and domain functional level **shall** be Windows Server 2022; downgrade is prohibited. |
| URS-ARCH-04 | H | R1 | DNS **shall** be AD-integrated; DNS scavenging configured; DNSSEC enabled on the `quartz.local` zone; DNS over HTTPS / TLS evaluated annually. |
| URS-ARCH-05 | H | R1 | Two read-only domain controllers (RODC) **shall** be deployed in the DMZ for branch sites; RODC **shall not** cache credentials of any tier-0 or tier-1 account. |
| URS-ARCH-06 | H | R1 | FSMO roles (Schema Master, Domain Naming Master, RID, PDC Emulator, Infrastructure) **shall** be placed on a documented DC pool with documented seizure runbooks. |
| URS-ARCH-07 | M | R2 | A development / pre-production forest (`quartz-dev.local`) is maintained in a separate network segment for GPO and schema-change rehearsal; the dev forest is **out of GxP scope**. |
| URS-ARCH-08 | H | R1 | Trust relationships **shall** be limited to documented business need; new trusts require Identity Approver pair sign-off and InfoSec review. |
| URS-ARCH-09 | M | R2 | DC operating-system baseline **shall** conform to DISA STIG (or Microsoft Security Baseline) with documented site-justified exceptions. |
| URS-ARCH-10 | H | R1 | Domain controllers **shall** run no other server role; bastion-only posture is enforced and verified during configuration scans. |

Architecture decisions intentionally favour blast-radius containment over operational convenience: a separate administrative forest, RODC in the DMZ, FSMO role placement on a documented pool with seizure runbooks, and a bastion-only posture for domain controllers all reflect the Microsoft Enterprise Access Model and the lessons learned from public AD-compromise incidents in regulated industries (e.g., the 2017 NotPetya pharma impact and the 2021 Kaseya-attached MSP intrusions).

### 5.2 Identity Lifecycle — Joiner / Mover / Leaver (JML)

The HRIS (Workday) is the sole authoritative source for joiner / mover / leaver. AD is a consumer of HRIS events — never a place where identity is invented. This direction-of-truth keeps the GxP unique-user-identity guarantee aligned with the company's employment records, and is what makes Part 11 § 11.100 (no reuse / reassignment) implementable at scale.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-JML-01 | H | R1 | User accounts **shall** be provisioned **only** via a documented joiner workflow originating from the HRIS (Workday); ad-hoc account creation by IT is prohibited and **shall** be technically blocked through delegated rights configuration. |
| URS-JML-02 | H | R1 | Account creation **shall** include attributes: `sAMAccountName`, `userPrincipalName`, employeeID (HR primary key), department, manager, location, contract-end-date (for fixed-term contracts), GxP-relevance flag. |
| URS-JML-03 | H | R1 | Leaver events from HRIS **shall** disable the account within **8 business hours** of the termination effective time; emergency terminations **shall** complete within **1 hour** of HR notification. (21 CFR Part 11 § 11.10(d) — limiting access.) |
| URS-JML-04 | H | R1 | After disable, accounts **shall** be retained in a `Disabled-Users` OU for **90 calendar days** for forensic / audit purposes, then deleted; `employeeID` **shall** never be reassigned (Part 11 § 11.100 — uniqueness; never reuse). |
| URS-JML-05 | H | R1 | Mover events from HRIS **shall** trigger an automated access review; group memberships not justified by the new role **shall** be revoked within **14 calendar days**, with manager + QA co-sign on retained exceptions. |
| URS-JML-06 | H | R1 | Fixed-term contract accounts **shall** have a forced `accountExpires` matching contract end; renewal **shall** require a documented HR change. |
| URS-JML-07 | H | R1 | Service accounts **shall** be created and managed via a separate workflow (URS-SVC-01..05); each service account **shall** have a documented owner role, target system, renewal date, and is **not** in scope of HRIS JML. |
| URS-JML-08 | H | R1 | Privileged accounts (tier-0 / tier-1) **shall** be administratively separate from the same individual's standard user account (Part 11 § 11.10(d) + § 11.100). |
| URS-JML-09 | M | R2 | Re-hire workflow: a re-joining employee **shall** receive a **new** `employeeID` and **new** AD account; no re-activation of the previous identity. |
| URS-JML-10 | H | R1 | Stale-account audit: accounts inactive ≥ 60 days **shall** raise a review; ≥ 90 days **shall** be disabled automatically pending manager confirmation. |

### 5.3 Authentication — Multi-Factor + Conditional Access

Authentication design is phishing-resistant by default. The historical reliance on passwords + SMS OTP is treated as a documented anti-pattern; FIDO2 / WebAuthn hardware keys, Windows Hello for Business, and Entra ID conditional access compose the primary authentication pathway. Conditional access is the policy decision point: it consumes signals (user, device, location, sign-in risk, user risk) and applies a documented matrix of allow / step-up / block actions. The full policy set is exhibited in the FS Configuration Specification.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUTHN-01 | H | R1 | All access to GxP applications **shall** require MFA enforced via Entra ID conditional access; legacy authentication protocols (POP, IMAP, SMTP-AUTH, basic auth) **shall** be blocked tenant-wide. (Part 11 § 11.10(d) + § 11.200(b).) |
| URS-AUTHN-02 | H | R1 | Tier-0 and tier-1 privileged accounts **shall** use FIDO2 phishing-resistant authenticators (WebAuthn hardware key) only; TOTP and SMS are explicitly disallowed for privileged authentication. |
| URS-AUTHN-03 | H | R1 | Standard users **shall** use FIDO2 by default; Microsoft Authenticator with number-matching is permitted as a fallback; SMS is **prohibited** as an MFA factor. |
| URS-AUTHN-04 | H | R1 | Conditional access **shall** evaluate user-risk + sign-in-risk (Entra ID Protection signals) at every authentication; high-risk sign-ins **shall** require step-up authentication or be blocked. |
| URS-AUTHN-05 | H | R1 | Device-compliance **shall** be a conditional-access requirement for GxP-application access from managed devices; unmanaged devices **shall** be blocked or routed through a session-controlled web access (Entra app proxy + Defender for Cloud Apps). |
| URS-AUTHN-06 | H | R1 | Re-authentication **shall** be required for sensitive operations downstream (e.g., e-signature per Part 11 § 11.200(a)) per the application's URS; AD / Entra ID **shall not** cache primary refresh tokens in a way that bypasses application-level re-auth. |
| URS-AUTHN-07 | H | R1 | Account lockout: 5 failed attempts in 15 minutes **shall** lock the account for 30 minutes; lockout events **shall** alert the SIEM and SOC. (NIST SP 800-63B § 5.2.2.) |
| URS-AUTHN-08 | M | R2 | Risk-based step-up: anomalous sign-ins (impossible travel, new country, anonymous IP) **shall** require step-up + DPO awareness for GDPR Art. 32 logging. |
| URS-AUTHN-09 | H | R1 | NTLM authentication **shall** be disabled domain-wide except for documented legacy exceptions; remaining NTLM use **shall** be monitored continuously via DC event 8004 + audit alerts. |
| URS-AUTHN-10 | H | R1 | LDAP signing + LDAP channel binding (LdapEnforceChannelBinding=2) **shall** be enforced on all DCs; unsigned LDAP is blocked. |
| URS-AUTHN-11 | M | R2 | Certificate-based authentication (CBA) **shall** be available for highest-assurance workflows (regulatory submission e-sign); managed by ADCS. |

### 5.4 Password and Credential Policy

Password policy is aligned to NIST SP 800-63B and explicitly rejects historically-prescribed but empirically-counterproductive practices (forced periodic rotation, complex composition rules requiring special characters). For privileged accounts the policy is stricter: vault-managed long random passwords, rotated on every PAM session, and ideally replaced by FIDO2 + certificate-based authentication. Loss-management procedures (Part 11 § 11.300(c)) cover stolen / lost FIDO2 hardware keys with same-day revocation + step-up re-enrolment.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PWD-01 | H | R1 | Password policy **shall** align to NIST SP 800-63B Memorized Secret recommendations: minimum length 14 characters; no composition rules forcing special characters; no scheduled rotation; rotation **only** on suspected compromise. (Part 11 § 11.300(b).) |
| URS-PWD-02 | H | R1 | Banned-password list **shall** be enforced (Microsoft Entra Password Protection + custom site list including company name, season+year patterns, and breached-credentials feed). (Part 11 § 11.300(d).) |
| URS-PWD-03 | H | R1 | Breached-credential blocking **shall** integrate with a reputable breach feed (HaveIBeenPwned API or equivalent); attempts to set a known-breached password **shall** be rejected. |
| URS-PWD-04 | H | R1 | Passwordless authentication (FIDO2 / Windows Hello for Business) **shall** be the default for users with managed devices; password fallback only when required by legacy applications. |
| URS-PWD-05 | H | R1 | Privileged accounts **shall** have a minimum length 20-character generated password vaulted in CyberArk; the password **shall** rotate after each use (PAM session). (Part 11 § 11.300(b) + § 11.100(b).) |
| URS-PWD-06 | H | R1 | Password recovery / reset **shall** require identity proofing per NIST SP 800-63A IAL2 (knowledge + possession factors); password reset via the service desk **shall** not bypass MFA enrolment for the next sign-in. |
| URS-PWD-07 | M | R2 | Service-desk password reset workflow **shall** be auditable; the operator's identity, the target account, the ticket reference, and the reset timestamp **shall** be logged and SIEM-forwarded. |

### 5.5 Authorization — RBAC / ABAC / Group Strategy

Authorisation is layered: AD groups are the system-of-record for role membership; downstream GxP applications evaluate group membership at sign-on (or via Entra ID app-role claims) to compute the user's permissions. Group naming, ownership, review cadence, and depth limits are all encoded so that an inspector can audit "who has access to what" via a single data join. Toxic-combination detection (e.g., author + approver of the same record type) runs through the IGA layer (§ 5.18) and feeds back to QA + InfoSec.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUTHZ-01 | H | R1 | GxP-application access **shall** be governed by AD groups named per the site naming convention (`GXP_<APP>_<ROLE>_<ENV>`); group purpose, owner, and review cadence **shall** be documented in the IAM register. |
| URS-AUTHZ-02 | H | R1 | Membership changes to GxP-application groups **shall** require an approved ticket recording role, business justification, approver identity, and effective dates. (Part 11 § 11.10(d) + § 11.10(g).) |
| URS-AUTHZ-03 | H | R1 | Role-conflict prevention: an individual **shall not** simultaneously hold author and approver roles for the same record type in a GxP application; AD **shall** expose group membership via a compliance-reporting view for downstream SoD checks. |
| URS-AUTHZ-04 | H | R1 | Quarterly access reviews **shall** run per GxP application; group owners certify membership; non-certified members **shall** be removed within 5 business days. |
| URS-AUTHZ-05 | H | R1 | Nested-group depth **shall** be capped at 4 to preserve auditability; nesting beyond 4 **shall** require Identity Approver pair sign-off. |
| URS-AUTHZ-06 | M | R2 | Attribute-based entitlements: where ABAC decisioning is delegated (e.g., Entra ID dynamic groups), the attribute set, source, and update cadence **shall** be documented and change-controlled. |
| URS-AUTHZ-07 | H | R1 | Group ownership **shall** be tied to a named role (not an individual); ownership changes **shall** be HR-event-driven. |
| URS-AUTHZ-08 | M | R2 | Group creation **shall** require business justification, an owner, a review cadence, and a planned end-of-life date for project-scoped groups. |
| URS-AUTHZ-09 | H | R1 | Application-team-managed groups **shall** be enforced via delegation in OUs; cross-team group modification **shall** be blocked at ACL level. |

### 5.6 Privileged Access Management (PAM)

PAM is the layer where most real AD compromise scenarios are stopped or accelerated. The combination of tier-0 isolation (PAW + administrative forest), JIT elevation (Entra PIM and CyberArk JIT), and brokered + recorded sessions (CyberArk Session Manager) implements defence-in-depth around the identity control plane. Standing tier-0 group membership is treated as a deviation requiring documented justification.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PAM-01 | H | R1 | Tier-0 administrative actions **shall** be performed only from a Privileged Access Workstation (PAW) in a hardened configuration; no tier-0 logon to standard workstations. |
| URS-PAM-02 | H | R1 | Tier-0 actions **shall** follow a break-glass procedure: ticket-driven, time-bounded (max 4 hours), justification recorded, with InfoSec witness during the session and retrospective review within 5 business days. |
| URS-PAM-03 | H | R1 | Domain Admins, Enterprise Admins, Schema Admins **shall** be empty by default; membership added only via JIT activation (Entra PIM or CyberArk JIT) and removed automatically at session end. |
| URS-PAM-04 | H | R1 | All tier-0 and tier-1 sessions **shall** be brokered through CyberArk PAM with credential vaulting and full session recording; recordings retained ≥ 1 year online + ≥ 7 years archived; tamper-evident storage. |
| URS-PAM-05 | H | R1 | Two break-glass tier-0 accounts **shall** exist with credentials stored in dual physical custody (two separate safes, dual-key); opening either safe **shall** trigger an immediate SOC alert + automatic ticket. |
| URS-PAM-06 | H | R1 | JIT elevation requests **shall** require approval from a second person not in the requestor's reporting chain; auto-approval is forbidden for tier-0. |
| URS-PAM-07 | H | R1 | Session recording **shall** capture command-line input, output, and screen video; recordings are encrypted at rest and chain-of-custody verified. |
| URS-PAM-08 | M | R2 | Privileged Access Workstations **shall** be hardened per Microsoft PAW guidance: AppLocker / WDAC allow-list; Defender ASR rules; no internet egress; no productivity software. |
| URS-PAM-09 | H | R1 | Privileged-account inventory **shall** be reviewed monthly; orphaned privileged accounts (no active owner) **shall** be disabled within 5 business days. |
| URS-PAM-10 | H | R1 | Vendor / third-party privileged access **shall** be brokered through CyberArk with named, time-bounded accounts; shared vendor accounts are prohibited. |

### 5.7 Service Accounts and Secrets

Service accounts are the single largest source of unaccounted-for AD risk in pharma estates: long-lived, often over-privileged, with passwords stored in scripts, configuration files, or worse. The site default is therefore Group Managed Service Accounts (gMSA) wherever the consuming product supports them, with CyberArk-vaulted alternatives + workload-identity federation for the remainder. Tier-0 privileges on service accounts are an absolute prohibition.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SVC-01 | H | R1 | All new service accounts **shall** be Group Managed Service Accounts (gMSA) where the consuming system supports it; AD automatically rotates the password on the configured interval. |
| URS-SVC-02 | H | R1 | Service-account credentials for non-gMSA-compatible systems **shall** be vaulted in CyberArk and rotated on a documented cadence (≤ 90 days for tier-1; ≤ 180 days for tier-2) or after any session use. |
| URS-SVC-03 | H | R1 | Service accounts **shall not** hold tier-0 privileges; service accounts **shall not** have interactive-logon rights to standard workstations. |
| URS-SVC-04 | H | R1 | Service accounts **shall** be denied membership in Domain Admins, Enterprise Admins, Schema Admins, and Account Operators. |
| URS-SVC-05 | H | R1 | Each service account **shall** map to a single named service / system; shared service accounts are prohibited (Part 11 § 11.100 uniqueness applied at machine-identity layer). |
| URS-SVC-06 | M | R2 | Service-account ownership **shall** be reviewed quarterly; orphaned service accounts **shall** be disabled within 30 days. |
| URS-SVC-07 | H | R1 | Workload-identity federation (Entra ID workload identities for Azure-hosted GxP applications) **shall** replace stored credentials where the platform supports it. |

### 5.8 Group Policy and Endpoint Configuration

GPO is treated as code: every change is reviewed in a pre-prod GPO test domain via AGPM-equivalent workflow, signed off by the Identity Approver pair, and rolled out through staged production deployment with a documented rollback path. BitLocker + LAPS + Defender ASR + AppLocker / WDAC together constitute the endpoint baseline; deviations from baseline trigger an investigation.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-GPO-01 | H | R1 | Workstation screen lock **shall** activate after ≤ 10 minutes of inactivity; AD re-authentication is required to unlock. |
| URS-GPO-02 | H | R1 | Removable-media write **shall** be restricted by GPO on GxP workstations; exceptions managed by ticket with InfoSec sign-off; read-only for vendor-provided media. |
| URS-GPO-03 | H | R1 | Office macros from internet origin **shall** be blocked by GPO across the site (consistent with Excel calculator URS — e.g., `LCN-URS-EXCEL-CU-001`). |
| URS-GPO-04 | H | R1 | Anti-malware (Microsoft Defender for Endpoint) **shall** be centrally managed via Intune + GPO; tamper-protection enabled; cloud-delivered protection on; ASR rules in block mode. |
| URS-GPO-05 | M | R2 | Workstation configuration drift detection (Defender configuration health + Intune compliance) **shall** report deviations to the IT operations dashboard weekly. |
| URS-GPO-06 | H | R1 | BitLocker full-disk encryption **shall** be enforced on every GxP workstation; recovery keys escrowed in AD / Entra ID and accessible only by service-desk under audit. |
| URS-GPO-07 | H | R1 | LAPS (Windows Local Administrator Password Solution) **shall** randomise the local-administrator password per workstation; passwords vaulted in AD with read access restricted to designated service-desk role. |
| URS-GPO-08 | H | R1 | PowerShell Constrained Language Mode **shall** be enforced on tier-2 endpoints; Just Enough Administration (JEA) endpoints on tier-1 / tier-0. |
| URS-GPO-09 | M | R2 | Software-installation restriction: only signed, allow-listed software (Intune + Defender Application Control) may run on GxP workstations. |
| URS-GPO-10 | H | R1 | GPO change control: every GPO modification **shall** be tied to a change request, reviewed in AGPM (Advanced Group Policy Management) or equivalent, tested in pre-prod, and approved by the Identity Approver pair before production deployment. |

### 5.9 Kerberos Hygiene and Protocol Hardening

The Kerberos hygiene subsection is dedicated to the well-known attack surface of the AD authentication protocol. Each requirement maps to a documented attack pattern (golden ticket → URS-KRB-01; silver ticket / pass-the-ticket → URS-KRB-02; downgrade to RC4-HMAC → URS-KRB-03; unconstrained delegation abuse → URS-KRB-05; Kerberoasting → URS-KRB-06..07; AS-REP roasting → URS-KRB-08). The corresponding mitigations are operationalised in monthly hygiene reviews.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-KRB-01 | H | R1 | The `krbtgt` account password **shall** be rotated twice with a 24-hour gap at least every 180 days, and immediately after any tier-0 personnel change (Golden-Ticket defence). |
| URS-KRB-02 | H | R1 | Kerberos ticket lifetimes **shall** be: user ticket 10 hours; renewable 7 days; service ticket 10 hours. Documented exceptions are recorded. |
| URS-KRB-03 | H | R1 | DES, RC4-HMAC, and MD5 encryption types **shall** be disabled domain-wide; AES-256 + AES-128 are the only permitted Kerberos encryption types. |
| URS-KRB-04 | H | R1 | "Account is sensitive and cannot be delegated" **shall** be set on all tier-0 accounts; Protected Users group **shall** include all tier-0 admins. |
| URS-KRB-05 | H | R1 | Unconstrained Kerberos delegation **shall** be prohibited; only constrained or resource-based constrained delegation (RBCD) is permitted, scoped to the minimum necessary services. |
| URS-KRB-06 | H | R1 | Service-Principal-Name (SPN) inventory **shall** be reviewed monthly; orphaned SPNs **shall** be removed. |
| URS-KRB-07 | M | R2 | Kerberoasting detection (anomalous service-ticket request volume) **shall** be a SIEM correlation rule with alert to SOC. |
| URS-KRB-08 | H | R1 | Pre-authentication **shall** be required for all accounts; AS-REP-roastable accounts (DONT_REQ_PREAUTH flag) **shall not** exist. |

### 5.10 Hybrid Cloud — Entra ID + Conditional Access

Entra ID is the cloud identity layer; conditional access is the centralised policy engine. The deployment uses password-hash-sync (PHS) rather than federated AD FS to remove a single-point-of-failure on-prem dependency: the site explicitly favours cloud-only continuity of SaaS authentication in the event of an on-prem AD outage. Emergency-access (break-glass) Global Admin accounts are cloud-only and exempt from MFA conditional-access (covered by physical safe + monitoring) so that the site retains a recovery channel even when MFA infrastructure is impaired.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HYB-01 | H | R1 | Hybrid identity sync from AD to Entra ID **shall** be performed by Entra ID Connect (or Entra Connect Cloud Sync) deployed in HA pairs; sync filter excludes service accounts and tier-0 accounts from cloud projection. |
| URS-HYB-02 | H | R1 | Password sync **shall** be implemented via password-hash-sync (PHS) with passwordless / FIDO2 as the primary cloud authenticator; pass-through-authentication and federated AD FS are not used to minimise on-prem dependencies. |
| URS-HYB-03 | H | R1 | Conditional access policy set **shall** include (at minimum): block legacy authentication, require MFA for all users, require compliant device for GxP apps, block high-risk sign-ins, require phishing-resistant MFA for privileged roles. |
| URS-HYB-04 | H | R1 | Entra ID Privileged Identity Management (PIM) **shall** govern eligibility, JIT activation, and approval for all cloud privileged roles (Global Admin, Privileged Role Admin, etc.); standing assignments are forbidden. |
| URS-HYB-05 | H | R1 | Entra ID logs (sign-in, audit, provisioning, risk events) **shall** stream to Splunk via Event Hubs within ≤ 5 minutes of generation. |
| URS-HYB-06 | M | R2 | Cloud-only privileged accounts (≥ 2 emergency Global Admin break-glass) **shall** exist as a recovery channel decoupled from on-prem AD compromise; credentials safe-stored under dual custody. |
| URS-HYB-07 | M | R2 | SCIM provisioning to SaaS GxP applications (LMS, eQMS, ePRO portal) **shall** be the standard provisioning channel; just-in-time provisioning on first SAML sign-on is permitted where SCIM is unsupported, with periodic reconciliation. |

### 5.11 PKI — ADCS and Signing-Certificate Issuance

ADCS is the on-prem PKI providing user, device, service, and code-signing certificates. The two-tier architecture (offline root + online issuing CAs) is the GAMP / ISO 27001 baseline. Root-CA keys are protected by FIPS 140-2 Level 3 HSM and operated under a witnessed key-ceremony procedure. Quantum-readiness is monitored — NIST FIPS 203 / 204 / 205 algorithms — but no operational migration is required in this URS revision.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PKI-01 | H | R1 | ADCS **shall** be deployed as a two-tier hierarchy: offline root CA (powered off, air-gapped) + two issuing CAs online; root-CA keys protected by FIPS 140-2 Level 3 HSM. |
| URS-PKI-02 | H | R1 | User signing certificates **shall** be issued per individual with 1-year validity; revocation propagated via CRL (≤ 1-hour publication interval) and OCSP. |
| URS-PKI-03 | H | R1 | Service / device certificates **shall** be issued via auto-enrolment templates; certificate templates **shall** be under change control. |
| URS-PKI-04 | H | R1 | Key-ceremony procedures (root-CA installation, key generation, signing of issuing-CA certificates) **shall** require ≥ 2 of 3 named PKI Operators physically present, video-recorded, and signed off by InfoSec. |
| URS-PKI-05 | M | R2 | Certificate-template change **shall** require change-control approval and pre-prod validation. |
| URS-PKI-06 | H | R1 | Quantum-readiness watch: a documented annual assessment **shall** evaluate post-quantum-cryptography (PQC) migration plans (NIST FIPS 203 / 204 / 205 algorithms); no operational obligation in this URS revision. |

### 5.12 Audit Trail and SIEM Forwarding

The audit trail is the regulatory backbone for Part 11 § 11.10(e) and Annex 11 § 9. AD audit forwarding is treated as a tier-1 service: gaps in forwarding generate operator alerts; the cold archive is write-once with cryptographic hash chain; a nightly integrity check protects against silent corruption. The SOC consumes the same stream for security correlation, and the regulatory inspector's view (filtered) is generated from the same source.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | AD **shall** log, at minimum: account-management events (create / modify / disable / delete); logon / logoff (success + failure); Kerberos authentication; group-membership changes (especially tier-0 + tier-1); GPO changes; schema changes; replication events; LDAP modifications; AD-recycle-bin operations. (Part 11 § 11.10(e).) |
| URS-AUD-02 | H | R1 | AD audit events **shall** be forwarded to the site SIEM (Splunk Enterprise Security) within ≤ 5 minutes of generation; gaps in forwarding ≥ 10 minutes **shall** raise alerts to on-call SOC within 15 minutes. |
| URS-AUD-03 | H | R1 | Audit-log retention: ≥ 1 year online in SIEM; ≥ 7 years in cold archive (Splunk Smart Store / S3 with Object Lock); tamper-evident through write-once index + cryptographic hash chain. |
| URS-AUD-04 | H | R1 | Tier-0 actions and break-glass usage **shall** be reviewed by the InfoSec Officer within 5 business days of occurrence; review evidence retained ≥ 7 years. |
| URS-AUD-05 | H | R1 | Audit-trail entries **shall** capture: timestamp (UTC, ms-precision); event ID; subject identity (SID + UPN); target object (DN); operation; outcome; originating IP + workstation. (Part 11 § 11.10(e) + Annex 11 § 9.) |
| URS-AUD-06 | H | R1 | Privileged-group membership changes **shall** generate a HIGH-priority SIEM alert routed to InfoSec within 1 minute. |
| URS-AUD-07 | M | R2 | A monthly attestation report **shall** be produced summarising AD audit volume, failed-forward events, and gaps; signed by Identity Services Lead. |
| URS-AUD-08 | H | R1 | Audit-log integrity verification **shall** run nightly (hash-chain validation); discrepancies **shall** raise a CRITICAL SIEM alert + InfoSec investigation. |

### 5.13 21 CFR Part 11 Sub-Section Alignment

This subsection consolidates Part 11 sub-section coverage. Each row binds an AD capability to the specific 21 CFR Part 11 § that depends on it. Downstream-application URSs that rely on AD-provided unique-user identity, authority checks, and audit substrate may reference this subsection rather than re-stating Part 11 in their own scope.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Part 11 § 11.10(a): the system **shall** implement procedures and controls (this URS + the IT change-management SOP) that protect the validity and reliability of authentication / authorisation records consumed by downstream GxP applications. |
| URS-PART11-02 | H | R1 | Part 11 § 11.10(b): identity-event exports for inspection readiness **shall** be available in human-readable form (PDF + CSV) and electronic form (JSON) for any user / system within retention. |
| URS-PART11-03 | H | R1 | Part 11 § 11.10(c): AD audit-trail records **shall** be protected throughout the retention period (URS-AUD-03) via SIEM immutability + cold-archive object-lock. |
| URS-PART11-04 | H | R1 | Part 11 § 11.10(d): access **shall** be limited to authorised individuals (URS-JML-* + URS-AUTHZ-* + URS-PAM-*); failed-access events are logged + alerted. |
| URS-PART11-05 | H | R1 | Part 11 § 11.10(e): the AD audit trail **shall** be operational, time-stamped (URS-AUD-05), and **shall not** obscure previously recorded information. |
| URS-PART11-06 | H | R1 | Part 11 § 11.10(g): authority checks (group / role membership) **shall** be enforced at every authentication and at downstream-application authorisation; AD provides the verified authority signal. |
| URS-PART11-07 | H | R1 | Part 11 § 11.10(k): AD-related operational manuals + change-control procedures **shall** be maintained under document control. |
| URS-PART11-08 | H | R1 | Part 11 § 11.30: open-system controls (Entra ID is an internet-exposed cloud component) — TLS 1.2+ enforced; FIDO2 / phishing-resistant MFA per URS-AUTHN-02..03; risk-based conditional access per URS-AUTHN-04. |
| URS-PART11-09 | H | R1 | Part 11 § 11.100: every account **shall** be uniquely associated with a single individual; identifiers (sAMAccountName, UPN, employeeID, SID) **shall never** be reused or reassigned (URS-JML-04). |
| URS-PART11-10 | H | R1 | Part 11 § 11.200(a): identity-based electronic signatures employ unique identifier + password (or PKI key) + biometric / FIDO2; AD provides the unique-identifier substrate and re-auth control (URS-AUTHN-06). |
| URS-PART11-11 | H | R1 | Part 11 § 11.200(b): biometric e-signatures **shall** be designed so they cannot be used by anyone other than their owner — enforced by FIDO2 device-bound credentials + Windows Hello biometric attestation. |
| URS-PART11-12 | H | R1 | Part 11 § 11.300(a): unique user-ID enforced (URS-JML-04 + URS-PART11-09). |
| URS-PART11-13 | H | R1 | Part 11 § 11.300(b): password / authenticator periodic checks per URS-PWD-01..03; breached-credential block per URS-PWD-03. |
| URS-PART11-14 | H | R1 | Part 11 § 11.300(c): loss-management procedures — lost FIDO2 keys reported within 1 business day; the key's certificate **shall** be revoked + the AD account flagged for step-up re-enrolment. |
| URS-PART11-15 | H | R1 | Part 11 § 11.300(d): transaction safeguards — failed-logon detection + lockout (URS-AUTHN-07); breached-credential rejection (URS-PWD-03). |
| URS-PART11-16 | H | R1 | Part 11 § 11.300(e): initial + periodic testing of tokens / authenticators — FIDO2 keys self-attest at enrolment; periodic device attestation through Intune compliance. |
| URS-AN11-01 | H | R1 | EU GMP Annex 11 § 12.1 — physical + logical access controls (URS-ARCH-* + URS-AUTHZ-* + URS-PAM-*). |
| URS-AN11-02 | H | R1 | EU GMP Annex 11 § 12.3 — system access reviews per URS-AUTHZ-04. |
| URS-AN11-03 | H | R1 | EU GMP Annex 11 § 9 — system-internal audit trail (URS-AUD-*). |
| URS-AN11-04 | H | R1 | EU GMP Annex 11 § 4.8 — backup of AD itself per URS-BAK-* (DR/BCP). |
| URS-AN11-05 | H | R1 | EU GMP Annex 11 § 7.2 — data-integrity demonstration for AD-restored content per URS-BAK-04. |

### 5.14 Cybersecurity, NIS2 and ISO 27001:2022

Cybersecurity scope for AD includes the obligations of NIS2 (Quartz Genomics is an essential entity per Annex I sector 5 — manufacture of medicinal products) and the ISMS controls of ISO/IEC 27001:2022. The site CISO is accountable for both. Identity compromise is the single highest-impact incident class for an essential pharma entity — the requirements below codify defence-in-depth across detection (BloodHound, Defender for Identity, SIEM correlation), isolation (tier-0 segmentation), reaction (incident playbook with AD scenarios), and reporting (NIS2 24/72-hour / 1-month timeline).

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CYB-01 | H | R1 | The system **shall** be operated within the site ISMS certified to ISO/IEC 27001:2022; Annex A controls A.5 (policies), A.8 (asset management), A.9 (access control), A.12 (operations security), A.16 (incident management), A.17 (continuity) **shall** be evidenced. |
| URS-CYB-02 | H | R1 | NIS2 Directive (EU) 2022/2555 — Quartz Genomics is classified as an *essential entity* (Annex I sector 5, manufacture of medicinal products). Cybersecurity risk-management measures per NIS2 Art. 21 **shall** apply to AD. |
| URS-CYB-03 | H | R1 | NIS2 Art. 23 incident reporting: significant incidents affecting AD **shall** be reported to the competent authority (BSI in DE; NCSC-UK in UK; OFCS / NCSC-CH in CH) within: **early warning ≤ 24 h**, **incident notification ≤ 72 h**, **final report ≤ 1 month**. (Detected from SIEM correlation; routed via the IM-on-call process.) |
| URS-CYB-04 | H | R1 | Attack-path defence: BloodHound-style attack-path enumeration **shall** be run quarterly; high-risk paths to tier-0 **shall** be remediated within 90 days. |
| URS-CYB-05 | H | R1 | Tier-0 isolation: the administrative forest **shall** be on a dedicated network segment with explicit firewalling; tier-0 PAW network egress is restricted to identity-management endpoints. |
| URS-CYB-06 | H | R1 | Phishing-resistant MFA + Zero-Trust signal evaluation per URS-AUTHN-02..05. |
| URS-CYB-07 | M | R2 | Penetration testing of the AD environment **shall** be performed annually by an independent qualified party; findings tracked to closure. |
| URS-CYB-08 | M | R2 | Red-team exercise (purple-team preferred) **shall** be conducted ≥ once every 2 years; tier-0 escalation paths are an explicit objective. |
| URS-CYB-09 | H | R1 | GDPR Art. 32 — security of processing: AD personal-data flows (employee directory) **shall** be documented in the Record of Processing Activities; DPO consulted on changes. |
| URS-CYB-10 | M | R2 | BSI IT-Grundschutz ORP.4 + APP.2.2 (Active Directory) **shall** be evidenced for the Munich (DE) site; gap remediations tracked. |
| URS-CYB-11 | H | R1 | Cyber-incident playbook **shall** include AD-compromise scenarios (golden ticket, DCSync, NTDS.dit theft, ransomware via privileged credential abuse); tabletop exercise annually. |
| URS-CYB-12 | M | R2 | Supply-chain security: AD-tooling vendors (CyberArk, Splunk, Microsoft, Tenable, Mandiant) **shall** be tracked in the vendor-risk register; critical vulnerabilities affecting them **shall** be evaluated within 5 business days. |

### 5.15 Backup, Disaster Recovery, Forest Recovery

AD backup and forest recovery are operated together with the Backup System URS (`AUR-URS-BACKUP-001` and any local equivalent). Forest recovery is a documented exercise — not an improvised one — because AD-aware backup + restore differs from generic file/VM backup: SYSVOL, FSMO ownership, krbtgt history, recycle-bin state, and DC metadata all need to be restored coherently, and restore validation has to demonstrate the system is back to a known-trustworthy state rather than back to a corrupted moment.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | System-state backups of every DC **shall** run nightly; retained ≥ 90 days online; immutable cloud copy retained ≥ 7 years. The backup service is consumed from `AUR-URS-BACKUP-001` / the equivalent local backup platform. |
| URS-BAK-02 | H | R1 | Forest-recovery runbook **shall** be documented per Microsoft's published forest-recovery guidance; tabletop exercise annually; full forest-restore test biennially in an isolated lab environment with documented evidence retained ≥ 7 years. |
| URS-BAK-03 | H | R1 | DC OS patching **shall** follow site change control; replication health **shall** be monitored continuously; replication-failure-to-resolution SLO ≤ 4 hours. |
| URS-BAK-04 | H | R1 | A documented AD restore-validation procedure **shall** demonstrate post-restore: schema integrity; SYSVOL replication; krbtgt continuity; FSMO role placement; recycle-bin functionality. (Annex 11 § 7.2.) |
| URS-BAK-05 | H | R1 | ADCS backup **shall** include the offline-root-CA hardware-key escrow, issuing-CA database, and certificate templates; restore tested biennially. |
| URS-BAK-06 | M | R2 | An air-gapped offline copy of essential AD state (last-known-good) **shall** be maintained for ransomware-resistance; refreshed monthly. |

### 5.16 Performance, Availability and Capacity

Authentication and authorisation are on the critical path of every GxP application's user experience. The non-functional targets (availability, latency, RPO, RTO) are documented here. Capacity is planned with 2× peak headroom and reviewed quarterly — under-capacity DCs are a documented pre-condition for cascading authentication failures in pharma estates.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AV-01 | H | R1 | Site availability target ≥ 99.95% (any DC reachable from any GxP-application server), measured per quarter. |
| URS-AV-02 | H | R1 | RTO from total DC loss at a single geography ≤ 4 hours via cross-site replication; full forest recovery RTO ≤ 72 hours. |
| URS-AV-03 | H | R1 | RPO for AD state: ≤ 24 hours (nightly system-state backup); for in-day directory changes, ≤ 1 hour (replication latency). |
| URS-PERF-01 | M | R2 | Authentication latency ≤ 200 ms at the 95th percentile under nominal site load (Kerberos AS+TGS round-trip on local-site DC). |
| URS-PERF-02 | M | R2 | LDAP-bind latency ≤ 100 ms at the 95th percentile from any GxP-application server to its primary DC. |
| URS-PERF-03 | M | R2 | DC capacity (CPU, memory, IOPS) **shall** support 2× projected peak load with headroom; capacity reviewed quarterly. |

### 5.17 Monitoring, Health and Operations

Monitoring covers the directory's operational health (replication, FSMO, KDC, capacity) and its security posture (privileged-group changes, anomalous Kerberos volume, conditional-access denials, sign-in risk). The same data feeds the IT Operations dashboard for daily ops review and the SOC's SIEM correlation rules. Synthetic transactions verify the user-visible identity path is healthy independently of operator-reported issues.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MON-01 | H | R1 | Continuous monitoring **shall** cover: replication health, DC heartbeat, FSMO availability, Kerberos KDC health, account-lockout volume, privileged-group changes, ADCS issuance + revocation rates, Entra Connect sync health, conditional-access policy denials. |
| URS-MON-02 | H | R1 | Alerts **shall** route by severity: CRITICAL to SOC + on-call within 1 minute; HIGH within 5 minutes; MEDIUM within 30 minutes. |
| URS-MON-03 | M | R2 | An operations dashboard (Grafana / PowerBI) **shall** surface KPIs (sign-in success rate, MFA challenge success, sign-in risk distribution, privileged-session count, replication lag) for daily review. |
| URS-MON-04 | M | R2 | Synthetic transactions (test user authentication + Kerberos ticket request) **shall** run every 5 minutes from each site; failures trigger an immediate alert. |

### 5.18 Identity Governance and Administration (IGA)

IGA closes the loop between AD as the identity store and the lifecycle / governance / certification process that keeps entitlements clean. Without IGA, group memberships accumulate over years and SoD becomes a paper compliance claim. With IGA, every entitlement carries an owner, a justification, an expiration (where appropriate), and a periodic review.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-IGA-01 | H | R1 | An identity-governance toolset (Microsoft Entra ID Governance or SailPoint) **shall** orchestrate access requests, approvals, reviews, and certifications across AD + Entra ID + SCIM-provisioned SaaS GxP applications. |
| URS-IGA-02 | H | R1 | Toxic-combination detection (e.g., user holds both "Batch-record author" and "Batch-record approver" entitlements across LIMS / MES / eQMS) **shall** run nightly and raise SoD findings to QA + InfoSec within 1 business day. |
| URS-IGA-03 | H | R1 | Access requests **shall** capture role, business justification, expiration (where appropriate), and ticket reference; approver chain **shall** be system-enforced. |
| URS-IGA-04 | M | R2 | A role-mining cycle **shall** run quarterly to surface drift between assigned entitlements and the documented role model; deviations addressed via the access-review workflow. |
| URS-IGA-05 | H | R1 | A Joiner / Mover / Leaver SLA dashboard **shall** track JML completion times against the URS-JML-* targets; missed SLAs reviewed monthly by Identity Services Lead + Head of QA. |

### 5.19 Third-party, B2B and Vendor Identity

External identities — partners, auditors, vendor support — are kept on a separate identity track via Entra ID B2B. Standing vendor accounts are prohibited; every vendor session is brokered through PAM with recording. Guest-access lifecycle (sponsorship, expiration, periodic review) is operationalised through the IGA layer.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-B2B-01 | H | R1 | External collaborators (contract auditors, regulatory inspectors with read-only access, vendor support engineers) **shall** be onboarded via Entra ID B2B with a sponsor, business justification, and time-bounded expiration not exceeding 12 months. |
| URS-B2B-02 | H | R1 | B2B guests **shall** require MFA at their home tenant **or** Quartz-enforced MFA; conditional access enforces the stricter requirement. |
| URS-B2B-03 | H | R1 | Vendor support sessions on production AD-joined systems **shall** be brokered through CyberArk PAM with full session recording; standing vendor accounts are prohibited (URS-PAM-10). |
| URS-B2B-04 | H | R1 | A documented guest-access review **shall** run quarterly; inactive ≥ 30 days **shall** be disabled; ≥ 60 days **shall** be removed. |
| URS-B2B-05 | M | R2 | Cross-tenant collaboration policies **shall** enumerate allowed partner tenants; default deny for any other domain. |

### 5.20 Data Protection, Privacy and Retention

AD processes employee personal data — name, contact details, organisational structure, manager, employment status. GDPR Art. 32 (security of processing) and the site Record of Processing Activities (Art. 30) govern this data. Where retention obligations under Part 11 § 11.10(c) conflict with right-to-erasure under Art. 17, the legitimate-interest basis (GxP integrity of audit records) is documented and is the controlling rule for identity-event audit trails.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DP-01 | H | R1 | The AD employee-directory schema **shall** carry only the attributes required for identity operations; sensitive personal data (e.g., health, race, religion) is forbidden in AD attributes. |
| URS-DP-02 | H | R1 | GDPR Art. 30 Record of Processing Activities (ROPA) entry for AD identity processing **shall** be maintained by the DPO; updated on material change. |
| URS-DP-03 | H | R1 | Audit-log access **shall** be restricted to named Auditor, SOC, and InfoSec roles; access events to audit logs are themselves audit-trailed (audit-of-audit). (GDPR Art. 32 + Annex 11 § 9.) |
| URS-DP-04 | H | R1 | Personal-data export for GDPR Art. 15 (right of access) requests on AD identity data **shall** be possible within statutory timelines through a documented procedure; coordinated with the DPO. |
| URS-DP-05 | M | R2 | Personal-data deletion / right-to-erasure (Art. 17) **shall** be applied to AD identity attributes within statutory timelines where the employment relationship has ended and statutory retention does not require continued processing. Note: identity-event audit trails are retained per Part 11 § 11.10(c) — this is a legitimate-interest override of Art. 17 documented in the ROPA. |
| URS-DP-06 | H | R1 | Cross-border transfer of identity data **shall** rely on documented Standard Contractual Clauses for non-EU regions; Entra ID tenant region pinned to EU where feasible. |

### 5.21 Training and Periodic Review

Identity-handling competence is a quality-system requirement. Training is role-specific (service desk vs. identity engineer vs. PKI operator vs. tier-0 admin) and re-issued on material procedure change. The annual periodic review consolidates evidence across configuration drift, audit-log integrity, access-review completion, deviation closure, recovery-test outcomes, NIS2 compliance status, and ISO 27001 surveillance findings.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Identity Engineers, Service-Desk Operators, PKI Operators, and tier-0 administrators **shall** complete role-specific training recorded in the LMS; retraining annually + on material procedure change. |
| URS-TRN-02 | M | R2 | A site-wide phishing-awareness + credential-hygiene programme **shall** run; results monitored; remedial training assigned where indicators fail. |
| URS-PR-01 | H | R1 | Annual periodic review covering: configuration drift, audit-log review evidence, access-review completion rate, deviation summary, recovery-test outcomes, NIS2-compliance status, ISO 27001 surveillance-audit findings; signed by Identity Services Lead + Head of IT + Head of QA + CISO. |
| URS-PR-02 | H | R1 | Quarterly access-certification campaigns **shall** run for every GxP application; non-certified memberships removed within 5 business days. |
| URS-PR-03 | M | R2 | Annual table-top exercise simulating AD compromise (golden ticket, DCSync) **shall** include InfoSec, IT, QA, and a senior business stakeholder; lessons learned captured in CAPA. |

### 5.22 Cross-System Integration (downstream consumers of AD)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-01 | H | R1 | AD **shall** be the authoritative authentication source for every GxP application at the site (LIMS, ELN, eQMS, EDMS, MES, SCADA, ePRO, Submissions, PV DB, Stability, SPC, RTRT, AI/ML Model Server, GenAI LLM Service, etc.), via Kerberos / LDAPS for on-prem or SAML 2.0 / OIDC via Entra ID for SaaS. |
| URS-INT-02 | H | R1 | AD **shall** be the authoritative role-membership source consumed by downstream-application authorisation evaluators. |
| URS-INT-03 | H | R1 | SCIM provisioning **shall** be the standard channel for user lifecycle into SaaS GxP applications (per app's URS); fallback to JIT provisioning is permitted with periodic reconciliation. |
| URS-INT-04 | H | R1 | AD **shall** be backed up by the centralised backup system (consumer of `AUR-URS-BACKUP-001`); restore-test cadence aligned to URS-BAK-04 + URS-TEST-* of the Backup URS. |
| URS-INT-05 | M | R2 | Outage of AD **shall** trigger the documented business-continuity playbook in the IT IM-process; downstream-application URSs document their AD-outage tolerance. |

## 6. Acceptance Criteria

The system **shall** enter validated GxP use when:

1. **CS** (Configuration Specification — domain / forest design, GPO baseline, conditional-access policy set, PAM topology), **RA** (Risk Assessment per ICH Q9(R1) + ISO 27005), **IQ** (infrastructure qualification of DC, RODC, ADCS, PAM, SIEM-forwarding pipeline), **OQ** (operational testing of authentication, authorisation, audit forwarding, JIT elevation, lockout, MFA challenge, conditional-access enforcement), and **PQ** (production performance + identity-lifecycle reflecting real HRIS feeds) are all approved and executed proportionate to GAMP Cat 3 conventions and ISPE GAMP GPG *IT Infrastructure Control and Compliance*.
2. PQ scenarios **shall** include: end-to-end joiner (HRIS → AD provisioning → SCIM downstream → group assignment); end-to-end leaver (HRIS terminate → 8-hour disable); mover-driven access review; tier-0 JIT activation with PAM session + recording; break-glass account opening + SOC-alert path; MFA enforcement on a GxP application; audit-log forwarding gap detection; replication-failure simulation; forest-recovery tabletop; ADCS root-CA key-ceremony witness; conditional-access policy block of a non-compliant device.
3. **VSR** (Validation Summary Report) approved by Identity Services Lead, Head of IT, Head of QA, CISO.
4. **RTM** (Requirements Traceability Matrix) maps every URS to ≥ 1 approved test case in IQ / OQ / PQ.
5. NIS2 incident-reporting workflow rehearsed with a documented dry-run to the competent authority.
6. ISO/IEC 27001:2022 surveillance audit completed with no Major non-conformities outstanding.

### 6.1 Validation Deliverables Inventory

The qualification dossier **shall** include (proportionate to GAMP Cat 3):

| Deliverable | Owner | Approver |
|---|---|---|
| FS — Functional Specification | IT Architect | Identity Services Lead + Head of IT |
| CS — Configuration Specification (forest, GPO, conditional access, PAM topology, ADCS templates) | Identity Engineer | Identity Approver pair + InfoSec |
| RA — Risk Assessment (per ICH Q9(R1) + ISO 27005, with NIS2 + GDPR overlays) | CSV Architect | Head of QA + CISO |
| IQ — Installation Qualification (DC / RODC / ADCS / PAM / SIEM-forwarding) | Identity Engineer | Validation Engineer |
| OQ — Operational Qualification (AuthN, AuthZ, MFA, lockout, JIT, audit forward) | Validation Engineer | Head of QA |
| PQ — Performance Qualification (production HRIS feed + downstream-app live tests) | Validation Engineer | Head of QA |
| VSR — Validation Summary Report | Validation Engineer | Identity Services Lead + Head of IT + Head of QA + CISO |
| RTM — Requirements Traceability Matrix (URS → FS → Test) | Validation Engineer | Head of QA |

## 7. Constraints

- Schema extensions and custom PowerShell automation that materially affects identity decisioning are out of Cat-3 scope; introducing them **shall** re-classify the affected component to Cat 5 and trigger custom-SDLC.
- Microsoft updates to AD DS, Entra ID, and ADCS are received through standard support channels; major version upgrades **shall** be change-controlled with rehearsal in the dev forest.
- No service account **shall** hold tier-0 privileges in production.
- The DR site **shall** be in a different power and network blast radius from the primary site.
- All cryptography **shall** meet FIPS 140-2 Level 2 (Level 3 for ADCS root-CA keys) and TLS 1.2 minimum; TLS 1.3 preferred.

## 8. Assumptions

- HRIS (Workday) is the source of truth for joiner / mover / leaver events and continues to expose its event API to the identity-provisioning pipeline with a verified SLA.
- The site SIEM is operational and retains logs per URS-AUD-03; SIEM-forwarding network availability is independent of AD authentication.
- Microsoft's published reference architecture for AD DS, the Enterprise Access Model, and the RED-forest pattern continue to be the implementation guides.
- CyberArk PAM and Microsoft Entra ID are themselves validated as GAMP Cat 3 vendor products and subject to vendor-validation evidence on file.
- The data-protection legal basis (GDPR Arts. 6(1)(b) / 6(1)(c)) for processing employee identity data is documented in the Record of Processing Activities.

## 9. References

**US — FDA + NIST:**
- 21 CFR Part 11 §§ .10(a/b/c/d/e/g/k), .30, .100, .200(a/b), .300(a/b/c/d/e)
- 21 CFR Part 211 § 211.68 (automatic, mechanical, and electronic equipment) — to the extent AD authenticates personnel operating Part-211 equipment
- NIST SP 800-63B — Digital Identity Guidelines: Authentication and Lifecycle Management
- NIST SP 800-63A — Identity Proofing
- NIST SP 800-53 Rev. 5 — Security and Privacy Controls (AC, AU, IA, SC families)
- NIST SP 800-207 — Zero Trust Architecture
- FDA Guidance on Data Integrity and Compliance with cGMP (2018)

**EU + DACH:**
- EU GMP Annex 11 §§ 4 (validation), 7 (data storage), 9 (audit trail), 12 (security)
- NIS2 Directive (EU) 2022/2555 — Arts. 21 (risk-management measures), 23 (incident reporting)
- GDPR Reg. (EU) 2016/679 Art. 32 (security of processing), Art. 33 (notification of breach)
- BfArM medicines + medical-device authority — for incident notifications affecting GxP-system access
- BSI IT-Grundschutz Kompendium — ORP.4 Identitäts- und Berechtigungsmanagement, APP.2.2 Active Directory, NET.1.1 Netzarchitektur und -design
- Swissmedic (CH) — for Basel DR-hub authority context
- TISAX — DACH information-security assessment (where applicable to pharma supply chain)

**International / Industry:**
- ISPE GAMP 5 (2nd Edition, 2022) — Category 3 conventions
- ISPE GAMP Good Practice Guide: *IT Infrastructure Control and Compliance*
- PIC/S PI 041 — Good Practices for Data Management and Integrity in Regulated GMP/GDP Environments
- ISO/IEC 27001:2022 — Annex A controls A.5, A.8, A.9, A.12, A.16, A.17
- ISO/IEC 27002:2022 — Information security controls
- ISO/IEC 27035 — Information security incident management
- ISO 22301:2019 — Business Continuity Management Systems
- ISO/IEC 24760-1:2019 — IT Security and Privacy — A framework for identity management
- ENISA — *Guidelines on supervision and enforcement under NIS2*

**Federal Office for Information Security (BSI, DE) — IT-Grundschutz modules:**
- ORP.4 — Identitäts- und Berechtigungsmanagement
- APP.2.2 — Active Directory Domain Services
- NET.1.1 — Netzarchitektur und -design
- SYS.1.1 — Allgemeiner Server
- CON.3 — Datensicherungskonzept (referenced for AD backup linkage)

**Vendor:**
- Microsoft — *Active Directory Domain Services Reference Architecture* (Windows Server 2022)
- Microsoft — *Securing Active Directory* — Enterprise Access Model / Tiered Administration / RED forest
- Microsoft — *Microsoft Entra ID Connect Documentation* + Entra Privileged Identity Management
- Microsoft — *Active Directory Certificate Services Best Practices*
- Microsoft — *Microsoft Defender for Identity*
- CyberArk — *Privileged Access Manager Architecture* + Session Manager
- Splunk — *Enterprise Security — Identity Datamodel + Threat-Detection content*

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

