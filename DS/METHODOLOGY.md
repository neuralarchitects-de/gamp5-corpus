# Methodology — How This DS Corpus Was Built

**Audience:** Quality Assurance leads, validation engineers, software architects, and IT compliance professionals in DACH pharma / biotech / medical-device organisations who need to know the provenance, regulatory grounding, and contamination posture of this Design Specification (DS) corpus before considering it for any internal use.

**TL;DR.** This corpus contains **50 Design Specifications** paired one-to-one with the URS+FS pairs published in `URS/_generated/final/` and `FS_FDS/_generated/final/`. Each DS is the third document in the GAMP 5 V-model — it describes **how the system is technically designed**, sitting between the FS (what the system functionally does) and the implementation (code, configuration, integration). The DS corpus was generated from publicly-available regulatory primary sources only — never from any client design, never from scraped or anonymised customer artefacts. Each document is structurally constrained to the GAMP-category-driven shape (Configuration Specification for Cat 4 / Software Design Specification for Cat 5 / Infrastructure Design Specification for Cat 1 / vendor-design-reliance statement for Cat 3), regulatorily anchored, and disclosed in machine-readable frontmatter as `ai_authored_disclosed` with `do_not_use_as: regulated_record`.

This file inherits the canonical rule-set (§ 2A.*) from `URS/_generated/final/METHODOLOGY.md` and `FS_FDS/_generated/final/METHODOLOGY.md` — the same citation-currency table, the same 21 CFR Part 11 sub-section map, the same ICH M10 / EU MDR PSUR / 21 CFR Part 58 GLP / DACH-authority / shall-must / YAML-frontmatter / GAMP-category-coherence / EU AI Act / Project Mode / Implementation Risk Register rules. § 2B (below) adds the **DS-specific** invariants: V-model placement, DS-vs-FS scope split, Cat-driven structure, the DS-side traceability rule (DS-IDs map to FS-IDs, mirroring the FS-IDs-map-to-URS-IDs pattern), and the no-source-code-redrawing rule.

---

## 1. Where the DS sits in the V-model

```
                       Verification side                    Validation side
                       ─────────────────                    ─────────────────

URS (user need / wish)  ◄────────── traced to ─────────►  User Acceptance Test (UAT) / PQ
        │                                                          ▲
        ▼                                                          │
FS (functional behaviour) ◄──────── traced to ─────────►  Functional Test / OQ
        │                                                          ▲
        ▼                                                          │
DS (technical design)    ◄──────── traced to ─────────►  Integration Test / Configuration IQ
        │                                                          ▲
        ▼                                                          │
Module Spec / Code      ◄──────── traced to ─────────►  Unit Test / Code Review
        │                                                          ▲
        └───────────────► implementation ───────────────────────────┘
```

- **URS** answers *what must the system do for the business*.
- **FS** answers *how does the system functionally satisfy each URS-ID* — observable behaviour, role-permission rules, named modules, integration partners (named).
- **DS** answers *how is the system technically designed to deliver that functional behaviour* — concrete configuration parameter values (Cat 4), module decomposition + algorithm + data-structure + interface-contract design (Cat 5), hardware / network / hardening topology (Cat 1), or a structured statement of reliance on vendor design documents (Cat 3).
- **Module Spec / Code** answers *how is a specific unit of code or configuration constructed* — only needed for Cat 5 site-developed systems.

GAMP 5 (2nd Edition, 2022) treats DS as a **technical expansion of the FS** — both hardware and software design are captured here. For Category 4 the DS narrows to a **Configuration Specification** (the controlled list of every configurable parameter, its chosen value, and the justification). For Category 5 the DS expands to a **Software Design Specification (SDS)** containing module decomposition, algorithm definitions, data-model design, and interface contracts, optionally with a separate Module Specification artefact for each unit of code.

Modern interpretations of GAMP 5 (per the 2nd-edition introduction of agile / iterative lifecycle models) allow the DS to be developed iteratively rather than in one big-design-up-front pass. This corpus presents the **canonical waterfall-style DS shape** as a structural reference — the same content can be authored across multiple agile increments and assembled into one DS at design-baseline time.

---

## 2. Generation pipeline

### 2.1 Architecture

The DS pipeline is parametrically identical to the URS+FS pipeline (see `URS/_generated/final/METHODOLOGY.md` § 1.1) — same regulatory primary-source pack, same system catalogue, same generation invariants, same post-generation validation gates. The difference is the **structural template**: the DS template enforces the V-model-position rules and the per-Cat shape rules listed in § 2B below.

### 2.2 Pipeline stages (delta vs URS+FS)

**Stage 1 — Regulatory primary-source pack.** Identical to URS+FS pipeline (FDA / EMA / ICH / ISPE / PIC/S / ISO / EU AI Act primary sources, hash-pinned).

**Stage 2 — System catalogue.** Identical to URS+FS pipeline; the DS is generated **one per existing URS+FS pair**, so the catalogue is implicit (= the list of 50 paired systems).

**Stage 3 — Per-document context pack.** For each DS, the pipeline assembles:
- The parent URS file (read for cross-check; DS does NOT directly cite URS-IDs)
- The parent FS file (the **authoritative input** — DS-IDs map to FS-IDs)
- The matching regulatory subset (same per-Cat binding as URS+FS)
- The DS structural-template prompt enforcing § 2B invariants

**Stage 4 — Generation invariants** (encoded in the prompt; **DS-specific delta** in bold):
- Every design item carries `(DS-ID, FS-ID it traces to, Priority H/M/L, Risk class R1/R2/R3, design statement)` — `shall`-clauses where the DS describes a designed behaviour; descriptive statements where the DS records a chosen configuration value or topology.
- **The DS-ID namespace is `DS-<DOMAIN>-NN` mirroring the FS-ID namespace; every DS-ID MUST trace to ≥ 1 FS-ID.** A DS-ID with no FS parent is an orphan and must be either removed or justified as a design-only concern (rare).
- **DS does NOT re-cite URS-IDs.** Traceability to the URS is transitive via the FS — the corpus's coupling-direction discipline (URS owns wishes; FS owns functional behaviour; DS owns technical design) keeps each artefact at its rightful abstraction level.
- **`shall` is the normative verb where the DS describes a designed behaviour** ("The configuration shall enforce ..." / "The module shall expose ..."). Descriptive design choices (chosen configuration values, chosen topologies, chosen algorithms) use indicative present ("The MasterControl Workflow `RELEASE_QC_RESULT` is configured with three review steps: ..."). `must` is reserved per the URS+FS rule (constraints on downstream consumers / quoted regulator text only).
- **GAMP category drives the DS shape** per § 2B.1 below. Cat 4 DS = Configuration Specification (parameter-value tables; vendor source code is NOT redrawn). Cat 5 DS = full SDS (modules + algorithms + data model + interfaces). Cat 3 DS = vendor-design-reliance statement (≤ 1 page, points to vendor design docs by name + version). Cat 1 DS = Infrastructure Design Specification (network / AD / NTP / backup topology + hardening baselines).
- **Vendor source-code design is NEVER re-drawn for Cat 4 systems.** The site DS for a Cat 4 system covers configuration, integration boundaries, and site-deployed components; vendor internals (e.g., MassLynx UI rendering pipeline, Veeva Vault page-layout code) remain the vendor's responsibility under vendor SDLC.
- **Configuration values cited in a Cat 4 DS MUST be real-product-realistic.** Where the FS names a Waters MassLynx 4.2 SCN1027 or LabWare LIMS 8 configuration table / role / signal / endpoint, the DS gives a value or value-range that is consistent with that product's actual configuration surface.
- **Each DS line cites the planned IQ / OQ / PQ test that verifies the design choice.** Same pattern as FS § 4 — each row carries a `Verified by` column.
- **DS frontmatter MUST include `parent_fs` block** (`document_number`, `version`, `file`) — the file path is relative to the DS file (e.g., `../../../FS_FDS/_generated/final/<file>`; from `DS/_generated/final/` the FS folder is three levels up + `FS_FDS/_generated/final/`). The transitive `parent_urs` block is included for convenience (read-only reference).
- **All other invariants (YAML rules, disclosure block, END marker, document-number convention) are identical to URS+FS.**

**Stage 5 — Per-document originality seed.** Inherits the URS+FS originality seed (same site / company / personnel fiction); the DS-specific seed adds: vendor product version exact build, chosen hosting/topology stance, chosen approach to configurable items where the FS leaves the choice open.

**Stage 6 — Post-generation validation.** Identical gates to URS+FS plus DS-specific:

| Check | What it verifies |
|---|---|
| YAML + disclosures | Same as URS/FS (per § 2A.9). |
| Stale-citation grep | Same as URS/FS (per § 2A.1–2A.6). |
| `shall`/`must` lint | `shall` for designed behaviour; `must` only on downstream consumers / quoted regulator text. |
| **DS↔FS traceability** | Every DS-ID in DS § 4 / § 5 / § 6 etc. appears in DS § N — DS → FS Traceability Matrix exactly once (no range compression). Every FS-ID referenced in the DS resolves to an FS-ID present in the paired FS. |
| **FS-namespace integrity** | FS-IDs cited by the DS exist in the paired FS § 4 + § 8. Orphan FS-IDs flagged. |
| **No URS-ID redrawing** | The DS body does NOT cite URS-IDs directly (only the frontmatter `parent_urs` block does). |
| **GAMP-Cat coherence** | Cat 4 DS contains § 4 Configuration Specification; Cat 5 DS contains § 4 Software Architecture + § N Module Specification table; Cat 3 DS is short + reliance-statement-shaped; Cat 1 DS contains Network / Identity / Backup topology. |
| **Tier-line floor** | T1 ≥ 200 L; T2 ≥ 400 L; T3 ≥ 700 L; T4 ≥ 1,000 L (per § 2B.3). |
| **END marker** | `END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.` present at file end. |

---

## 2A. Inherited canonical rule-set

§ 2A.1–2A.16 from `URS/_generated/final/METHODOLOGY.md` apply verbatim to this DS corpus. Restated in summary form here so a DS reader can verify compliance without a context switch; refer to the URS METHODOLOGY for the authoritative full text:

- § 2A.1 — Citation currency table (FDA / EU / ICH / DACH / vendor). Re-verify at every generation run.
- § 2A.2 — 21 CFR Part 11 sub-section map (only `.10 / .30 / .50 / .70 / .100 / .200 / .300` exist).
- § 2A.3 — ICH M10 section map (no `§ 6.1.3` / `§ 6.4` / `§ 6.6`).
- § 2A.4 — EU MDR PSUR cadence (Class IIb + III + implantables annual; IIa biennial; Class I uses PMSR per Art. 85).
- § 2A.5 — 21 CFR Part 58 GLP role rules (no `§ 58.33(b)` defines-PI).
- § 2A.6 — DACH authority map (BfR + Länder = DE GLP; BfArM = DE medicines + devices, NOT GLP).
- § 2A.7 — URS↔FS traceability lives in FS § 4 + § 8 only — URS Appendix A is forbidden.
- § 2A.8 — `shall` for system / designed behaviour; `must` only for downstream-consumer constraints or quoted regulator text.
- § 2A.9 — YAML frontmatter rules: quote strings with `:`, `;`, em-dash; `do_not_use_as` must contain `regulated_record`; `labelling.source_risk` must equal `ai_authored_disclosed`.
- § 2A.10 — GAMP-category-coherence rule.
- § 2A.11 — EU AI Act high-risk obligations checklist (Arts. 9–18, 26, 43, 47–49, 50, 72, 73, 99).
- § 2A.12 — URS structure invariants + filename version convention.
- § 2A.13 — Tier system (T1 / T2 / T3 / T4).
- § 2A.14 — EU AI Act Annex I (2027) vs Annex III (2026) classification rule.
- § 2A.15 — Project Mode declaration rule (URS Document Control line under System Class).
- § 2A.16 — FS § N Implementation Risk Register rule (implementation/integration/configuration/operational risks live in FS, NOT URS).

---

## 2B. DS-specific invariants

### 2B.1 GAMP-category-driven DS structure

The DS shape is **driven by the GAMP category** of the parent URS+FS. The category is declared in the DS Document Control block (mirroring the URS Project Mode line) and the structure MUST follow the matrix below.

| Cat | DS variant | Mandatory sections (in addition to common preamble — frontmatter, doc control, revision history, definitions, § 1 Purpose, § 2 Scope, § 3 Architectural Overview, § N References, § N+1 DS → FS Traceability Matrix, § N+2 Design-level Risk Register, END marker) | Forbidden content |
|---|---|---|---|
| **Cat 1 — Infrastructure** | **Infrastructure Design Specification (IDS)** | § 4 Network Topology + IP Plan; § 5 Identity + Authentication Design (AD / LDAP / Kerberos); § 6 Time Synchronisation (NTP topology); § 7 Backup + Storage Tier Design; § 8 Hardening Baseline (CIS / DISA STIG / BSI IT-Grundschutz references) | IQ/OQ/PQ test instructions for the infra itself (infrastructure is **qualified**, not validated like an application — cite infrastructure-qualification protocol IDs by reference only). |
| **Cat 3 — Non-Configurable COTS** | **Vendor-Design-Reliance Statement** | § 4 Vendor Design Documentation Inventory (titles, versions, controlled-document references); § 5 Site-Specific Integration Design (network / AD / file-share bindings); § 6 Site-Specific Configuration (the small set of site-level choices — site name, user-list, time-zone, etc.) | Re-drawing of vendor internals. Cat 3 DS is intentionally **thin** — the vendor's own design documents are the authoritative design; the site's DS adds only the binding context. |
| **Cat 4 — Configured Product** | **Configuration Specification (CS)** | § 4 Configuration Specification (per-CI rows — every configurable parameter, chosen value, default-vs-custom, justification, change-control reference); § 5 Workflow + Business-Rule Design (configured workflow names + steps + role-bindings + decision points); § 6 Role-Permission Matrix Design (table of every role × every permission); § 7 Integration Design (per-interface — endpoint, protocol, message schema, retry, error-handling, monitoring); § 8 Site-Deployed Components Design (if any site-developed code exists — scripts, custom reports, integration adapters — these get their own mini-SDS sub-section) | Vendor source-code internals (vendor's SDLC owns those). Re-statement of FS-line text — the DS adds the specific configuration value, not a paraphrase of the FS row. |
| **Cat 5 — Custom / Site-Developed** | **Software Design Specification (SDS)** | § 4 Software Architecture (logical view — components, layers, technology stack); § 5 Module Decomposition (per-module — responsibility, interface, dependencies); § 6 Data Model Design (DB schema, message schemas, file schemas, retention design); § 7 Algorithm + Calculation Design (per-algorithm — input/output, formula, edge cases, numerical precision); § 8 Interface + API Design (per-endpoint — method, path, auth, request/response schema, rate limits, error codes); § 9 Security Design (authN, authZ, key management, secret rotation, transport security, audit-trail emission design); § 10 Deployment Architecture (container/VM topology, orchestration, scaling, observability); § 11 Module Specification Table (per-module bullets — class names, file paths, unit-test references) | Mixing requirements (DS describes design, not need). Pseudocode is allowed for algorithm specs; full source code is not (the source is owned by the code repository, not the DS). |

The above per-Cat sections are **additive** to the common preamble + tail. The numbering shown is the canonical pattern; actual DS files may use locally-coherent numbering provided every mandatory section is present.

### 2B.2 DS-ID → FS-ID traceability rule

Mirrors the URS-ID → FS-ID rule (§ 2A.7) one level down:

1. **The DS is FS-namespace-dependent.** Each DS-ID names a design choice that implements one or more FS-IDs. The DS does NOT cite URS-IDs directly in its body — the URS link is transitive via the FS.
2. **Every DS-ID in the DS body MUST appear individually in DS § N — DS → FS Traceability Matrix as its own row.** No range compression — each ID gets its own row with the FS-ID it traces to.
3. **DS § N (Traceability Matrix) is the SOLE DS↔FS traceability surface in the corpus.** Inspectors auditing design traceability read DS § N.
4. **An FS-ID that has no DS-ID covering it MUST be flagged** in the DS Revision History as either (a) deferred-to-next-iteration design or (b) requires-vendor-only-design (Cat 3/Cat 4 vendor internals).
5. **A DS-ID with no FS-ID** is an orphan — either remove it or justify it as a design-only concern (e.g., a deployment-environment choice that is not tied to any specific FS-ID but is required for the system to be installed at the site).

### 2B.3 Tier-based DS line-count + design-item-count target

The DS scales with the parent URS+FS tier (the same T1/T2/T3/T4 system the URS+FS uses):

| Tier | System character | DS design-item count | DS line target |
|---|---|---|---|
| **T1 — Small / simple instruments + utilities + Cat 1 infra** | Cat 3 standalone instruments (Karl Fischer, particle counter); Cat 1 infra (Backup, AD when small) | **15–30 design items** | 200–350 L |
| **T2 — Standard lab instruments + mid-complexity Cat 4** | UV-Vis, NIR, dissolution, autoclave, tablet coater, Cat 4 standalone apps | **30–60 design items** | 400–600 L |
| **T3 — Large enterprise systems** | LIMS, ELN, eQMS, EDMS, RIM, RTRT, production SCADA, large pharma application platforms | **60–120 design items** | 700–1,100 L |
| **T4 — Mission-critical / multi-module + Cat 5 custom** | EDC, CTMS, eTMF, Vault Submissions, MES PAS-X, AI/ML Model Server, GenAI LLM Service, Pharmacovigilance DB, Tessera CV | **120–250 design items** | 1,000–1,800 L |

The tier of a DS is **inherited from the tier of the parent URS+FS pair** — a DS does not get to choose a tier independently. Tier choice is recorded in the DS Revision History as "Inherited Tier T<N> from parent URS+FS pair."

### 2B.4 Cat 4 Configuration Specification — content rules

A Cat 4 DS § 4 Configuration Specification carries one row per configuration item. The table shape is:

| CI-ID | Configuration item (named per vendor) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|

Rules:

1. **Per-vendor-named CIs only.** Use the actual vendor configuration-item name as it appears in the vendor's configuration manual or admin guide. "MassLynx Sample-List Approval Mode: `Two-Level` (Reviewer + Approver)" — not "Approval Workflow: Configured".
2. **Default-vs-custom flag.** Mark every chosen value as `Default` (vendor-recommended out-of-the-box) or `Custom` (site-specific deviation). Custom values must carry a justification line.
3. **Justification.** One sentence per CI explaining why the chosen value satisfies the bound FS-ID(s). Generic "for compliance" is not acceptable — name the specific compliance need (e.g., "21 CFR Part 11 § 11.50 e-signature manifestation").
4. **Range CIs are a single row** (e.g., `Password Length Min: 12`); enumeration CIs are a single row (e.g., `Audit Trail Filter: All Critical Events + Login + Approve + Reject`). Per-record permission matrices live in § 6 Role-Permission Matrix Design, not in § 4.
5. **Workflow + business-rule items get their own section** (§ 5 Workflow + Business-Rule Design) — these are too rich for a one-cell value column.
6. **Site-developed code inside a Cat 4 system** (custom integration scripts, custom reports, Excel-VBA macros) gets its own mini-SDS sub-section. Per GAMP 5 2nd ed., embedded custom code escalates a Cat 4 system to a hybrid Cat 4 + Cat 5 — the SDS sub-section follows the Cat 5 rules in § 2B.5.

### 2B.5 Cat 5 Software Design Specification — content rules

A Cat 5 DS § 4–§ 11 follow the Software Design Specification rules from GAMP 5 (2nd Ed.) + IEC 62304 / ISO 13485 alignment where the system is SaMD:

1. **§ 4 Software Architecture** — logical view (components + responsibilities + interactions); process view (deployment containers + replicas + scaling); technology view (language, framework, version, license). One ASCII diagram per view.
2. **§ 5 Module Decomposition** — per-module table: ID, name, responsibility, interface (what it exposes), dependencies (what it consumes), owner (team or repo), GxP-criticality (R1/R2/R3 inherited from FS).
3. **§ 6 Data Model Design** — database schema (table names, key columns, constraints, retention rule, encryption-at-rest mode); message schemas (per integration partner — typically JSON-schema or AVRO); file schemas where files are exchanged; data classification (PHI / PII / GxP / non-GxP).
4. **§ 7 Algorithm + Calculation Design** — per algorithm (named): input domain, output, formula or stepwise procedure, numerical-precision note, edge-case handling, reference (paper / regulator guidance / pharmacopeia where applicable). Pseudocode allowed, full source code not.
5. **§ 8 Interface + API Design** — per endpoint: HTTP method + path, authN method, request schema, response schema, rate limit, error codes + HTTP status mapping, idempotency, audit-trail-event emitted. OpenAPI-style table is preferred.
6. **§ 9 Security Design** — authN flow (sequence), authZ model (role / attribute / claim mapping), secret management (named secret store, rotation cadence), transport security (TLS version, cipher suite floor), audit-trail event taxonomy.
7. **§ 10 Deployment Architecture** — container / VM topology, orchestration (Kubernetes / OpenShift / VM-host), scaling policy, observability stack (logs, metrics, traces, SIEM target), disaster recovery design (RPO / RTO + restore-from-cold sequence).
8. **§ 11 Module Specification Table** — pointer table: per module, the file path / class / function and the unit-test reference. The full Module Specification artefact lives downstream as `<DOC-PREFIX>-MS-<DOMAIN>-NN`; the DS only references it.

### 2B.6 Cat 3 Vendor-Design-Reliance Statement — content rules

A Cat 3 DS is intentionally **thin** (≤ 300 lines typically; sometimes ≤ 200 for very small instruments). Content:

1. **§ 4 Vendor Design Documentation Inventory** — table: vendor design-doc title, version, document number (vendor-side), controlled-document reference at the site (DMS link), retention class.
2. **§ 5 Site-Specific Integration Design** — the small site-specific bindings: network attachment, AD binding (if any), file-share locations, NTP source, anti-malware policy. Per-CI rows as in § 2B.4.
3. **§ 6 Site-Specific Configuration** — the small list of site-level configuration choices the instrument supports out-of-the-box (site name, units, time-zone, default user list, calibration cadence). Per-CI rows as in § 2B.4.
4. **§ N Design-level Risk Register** — risks specific to the site's integration of the instrument (NOT vendor-internal risks; those live in vendor documentation).
5. **No re-drawing of vendor internals.** Vendor SDLC owns the firmware/embedded design — the site DS does not duplicate it.

### 2B.7 Cat 1 Infrastructure Design Specification — content rules

A Cat 1 DS is **topology-and-baseline-focused**:

1. **§ 4 Network Topology + IP Plan** — diagram (text), VLAN / subnet / IP-range plan, firewall posture (deny-by-default, named allow-rules at boundaries).
2. **§ 5 Identity + Authentication Design** — AD forest / domain structure, group-naming convention, Kerberos / LDAPS endpoints, MFA enforcement points.
3. **§ 6 Time Synchronisation (NTP)** — stratum-1 source, internal NTP topology, drift-monitoring threshold.
4. **§ 7 Backup + Storage Tier Design** — tier (T1 = mission-critical / RPO ≤ 1 h / RTO ≤ 4 h; T2 = important / RPO ≤ 4 h / RTO ≤ 24 h; T3 = archival / RPO ≤ 24 h / RTO ≤ 72 h), encryption-at-rest mode, WORM / immutability stance.
5. **§ 8 Hardening Baseline** — CIS Benchmark / DISA STIG / BSI IT-Grundschutz reference per platform; deviation register.
6. Cat 1 DS does NOT include IQ/OQ/PQ for the infrastructure itself — infrastructure is **qualified** via infrastructure-qualification protocols (cited by reference only).

### 2B.8 DS Design-level Risk Register

Mirrors the FS Implementation Risk Register (§ 2A.16). DS-level risks are **design-stage** risks — risks that originate in design choices, not in user wishes (URS) or functional behaviour (FS) or implementation defects (which are caught in IQ/OQ/PQ). Examples:

- A configuration choice that satisfies one FS-ID but creates a permission gap on an unrelated workflow (Cat 4)
- A module-decomposition choice that creates a hidden cross-module dependency (Cat 5)
- A network-topology choice that puts a GxP system in the same VLAN as a non-GxP system, weakening segmentation (Cat 1)
- A vendor-version pin that becomes unsupportable at end-of-life (any Cat)

Per-design-item GxP criticality (R1/R2/R3) is inherited from the parent FS-ID and is NOT duplicated in this register.

The full formal Risk Assessment (FMEA / HAZOP) remains a separate downstream artefact (`<DOC-PREFIX>-RA-<NN>`); the DS Design-level Risk Register is a **design-stage seed** for the formal RA, not a substitute.

### 2B.9 DS document-structure invariants

Every DS MUST contain, in this order:

1. YAML frontmatter (per § 2A.9) with `parent_fs` block (mandatory) and `parent_urs` block (informational; mirrored from parent FS).
2. H1 title `# Design Specification (DS)` or `# Configuration Specification (CS)` (Cat 4) or `# Software Design Specification (SDS)` (Cat 5) or `# Infrastructure Design Specification (IDS)` (Cat 1) or `# Design Specification (Vendor-Design-Reliance Statement)` (Cat 3).
3. H2 system title `## <System name> — <Vendor product or descriptor>` (matches FS H2).
4. Document Control table (Author / Reviewer(s) / Approver(s) — Solution Architect; Validation Engineer; QA Reviewer; System Owner; Process Owner; Security Architect for Cat 5/AI; SME (e.g., Mass-Spec Lead) for Cat 3/4 lab instruments).
5. Design Control block:
   - **Document Number** (`<PREFIX>-DS-<DOMAIN>-NNN`).
   - **Version** (starts at `1.0` for DS corpus v1.0 ship).
   - **Effective Date** *(synthetic)*.
   - **Parent FS** (document number + version).
   - **Parent URS** (informational; document number + version).
   - **Site** (matches FS).
   - **System Class (GAMP 5, 2nd ed.):** (matches FS).
   - **Project Mode:** (mirrored from parent URS — per § 2A.15).
   - **Regulatory Scope** (matches FS).
6. Revision History table.
7. Definitions table (DS-specific terms only; inherited URS+FS definitions by reference).
8. § 1 Purpose.
9. § 2 Scope (in / out — must mirror FS § 2 plus DS-specific boundary statements).
10. § 3 Architectural Overview (more detailed than FS § 3; includes one or more ASCII diagrams).
11. **§ 4 onwards — per-Cat sections per § 2B.1.**
12. **§ N — References** (organised by jurisdiction — US / EU / DACH / International / Vendor).
13. **§ N+1 — Appendix A — DS → FS Traceability Matrix** (one row per DS-ID).
14. **§ N+2 — Design-level Risk Register** (per § 2B.8).
15. END marker: `END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.`

**Filename version convention.** Every DS corpus file is named `<descriptive_slug>_DS_v<X.Y>.md`. The corpus ships at `v1.0`; the suffix tracks the current content revision per the same rule as URS / FS (§ 2A.12). The Document Number inside the file (`<PREFIX>-DS-<DOMAIN>-NNN`) is the stable identifier across revisions.

### 2B.10 Cross-document coherence (URS / FS / DS triple)

Every URS-ID in the parent URS:
- MUST be addressed by ≥ 1 FS-ID in the parent FS (§ 2A.7).
- MUST be addressed transitively in the DS — i.e., every FS-ID that traces to a URS-ID MUST itself be covered by ≥ 1 DS-ID, OR the DS Revision History flags the FS-ID as deferred-to-next-design-iteration (with rationale).

A DS does NOT need to cover FS-IDs that describe vendor-internal behaviour for which the site has no design surface (e.g., MassLynx UI rendering internals). These FS-IDs are marked in the DS Revision History as "vendor-internal — no site design surface" and excluded from the DS coverage count for traceability scoring.

The DS Revision History MUST report the DS coverage percentage in its initial-issue entry (e.g., "DS covers 94/100 FS-IDs; 6 FS-IDs flagged as vendor-internal — no site design surface").

---

## 3. Regulatory grounding (inherited)

Identical to URS+FS — see `URS/_generated/final/METHODOLOGY.md` § 2 for the full framework list (FDA / EMA / ICH / ISPE / PIC/S / ISO / DACH-specific authorities). Every DS references the same per-Cat regulatory subset its parent FS references; no DS introduces a new framework that the FS does not already bind.

DS-specific regulator-document binding notes:

- **Cat 4 DS — vendor configuration manuals.** A Cat 4 DS legitimately cites the vendor's configuration manual / admin guide / system-administrator reference by exact title + version. Examples: Waters MassLynx 4.2 SCN1027 *System Administrator Guide*; LabWare LIMS 8 *Configuration Reference*; Veeva Vault Submissions *Implementation Guide*. These citations live in § N References under "Vendor."
- **Cat 5 DS — software-engineering standards.** A Cat 5 DS legitimately cites IEC 62304 (medical device software lifecycle), IEC 81001-5-1 (security of health software), ISO/IEC/IEEE 12207 (software-life-cycle processes), and software-engineering-specific frameworks (OWASP ASVS, OWASP LLM Top 10, NIST SP 800-218 SSDF, SLSA). These citations live in § N References under "International."
- **Cat 1 DS — infrastructure standards.** A Cat 1 DS legitimately cites CIS Benchmarks, DISA STIG, BSI IT-Grundschutz (DACH context), NIST SP 800-53, ISO/IEC 27001:2022, ISO/IEC 27002. These citations live in § N References under "International" / "DACH."

---

## 4. Contamination guarantee (inherited)

Identical to URS+FS — see `URS/_generated/final/METHODOLOGY.md` § 3. The DS corpus was NOT generated from any client design document, any anonymised customer artefact, or any scraped internal-IT-team-design. The four verification mechanisms (read-only source pack, open-source pipeline, per-document YAML disclosure, fictional-identifier audit) apply identically.

---

## 5. License posture (inherited)

Identical to URS+FS — CC-BY-SA 4.0 for the dataset; Apache 2.0 for the pipeline and the methodology. See `URS/_generated/final/METHODOLOGY.md` § 5.

---

## 6. Eval rubric (DS variant)

Mirrors the URS+FS eval rubric philosophy: the DS is **useful** if its output is consistently a credible *first-draft technical-design starting point* that a competent solution architect / validation engineer can iterate on without rewriting from scratch. See `DS/_generated/final/EVAL_RUBRIC.md` for the full machine-readable 6-dimension scoring rubric (structural completeness, regulatory accuracy, GAMP-category coherence, design-item testability/verifiability, DS↔FS traceability, shall/must discipline).

---

## 7. Open follow-ups (post-v1.0 DS corpus)

- **Module Specifications** for Cat 5 systems — separate downstream artefact (`<DOC-PREFIX>-MS-<DOMAIN>-NN`) pointed to by the DS § 11 table; not in scope for v1.0.
- **Configuration Items reference list** — a corpus-wide vendor-CI inventory aggregated from all Cat 4 DSs, suitable as input to vendor-configuration audits.
- **Algorithm appendix** — pseudocode + numerical-precision specs collected from all Cat 5 DS § 7 sections, suitable as input to a downstream computational-verification artefact.
- **DS → IQ/OQ/PQ planned-test inventory** — aggregate Verified-by columns into a corpus-wide test plan.
- **Diff-against-parent-FS report** — automated check that every FS-ID present in the FS is either covered, deferred, or flagged-vendor-internal in the DS Revision History.

---

**Methodology version:** 1.1 · **Released:** 2026-05-16 · **License:** Apache 2.0

---

## 8. Changelog

### v1.1 — Codex review patch (2026-05-16)

Independent quality-review pass by Codex (OpenAI) on the v1.0 release surfaced 3 HIGH + 3 MED + 2 LOW findings. All HIGH + MED items patched before v1.1 promotion. Categories of defect found, all now fixed:

- **HIGH-1: Broken parent paths.** Frontmatter `parent_fs.file` + `parent_urs.file` paths used `../../...` but the DS files live at `DS/_generated/final/` — the correct relative path is `../../../...` (three levels up to `sample-gamp-docs/`, then down into `FS_FDS/_generated/final/` or `URS/_generated/final/`). Fixed in all 36 affected files. Methodology § 2.2 path example also corrected.
- **HIGH-2: Cat 3/Cat 4 contradiction.** Indus Karl Fischer + Drumlin Particle Counter declared "Category 4 — Configured Product" in their System Class block but used the Cat 3 Vendor-Design-Reliance Statement shape. Both files reframed to "Category 3 — Non-Configurable COTS" with matching Project Mode wording, restoring per-Cat coherence per § 2A.10.
- **HIGH-3: EU AI Act Annex I penalty tier overstated.** Hesperia RTRT cited the Art. 99 penalty cap as "€35M / 7% global turnover" on 4 lines — that tier applies only to prohibited Art. 5 practices. Annex I high-risk non-compliance is "€15M / 3% global turnover" per Art. 99(3). All 4 occurrences corrected with explicit note clarifying when the higher tier would apply.
- **MED-1: URS-IDs in DS body.** 10 DS files cited URS-IDs in body Justification columns, violating the DS↔FS-only traceability rule in § 2B.2. 109 body references stripped corpus-wide (URS coupling remains transitive via frontmatter `parent_urs` block). Files affected: Cassia SCADA Water, Cetus Watson LIMS, Hesperia RTRT, Kymeta PI Historian, Marigold EDC Rave, Phlox CMMS, Pyxis EMS, Selene Cold Chain, Vela Autoclave, Veridian MES PAS-X, Vesper Cleaning Val.
- **MED-2: Art. 50 transparency omission.** Tessera CV listed EU AI Act Arts. 8–21, 26, 43, 47–49, 72, 73, 99, 113 in its Regulatory Scope + References but omitted Art. 50 (transparency to natural persons — AI-generated content labelling). Added on both lines.
- **MED-3: CIS K8s Benchmark version-specific citations.** 4 Cat 5 SDS files (Hydra, Helios, Lyrae, Tessera) cited "CIS K8s Benchmark v1.9" — version-specific lock-in not externally verifiable at corpus release. 8 occurrences rewritten as "CIS Kubernetes Benchmark (current release at site deployment)" to defer version pin to the deploying site.
- **LOW-1: README Cat-listing inconsistency.** Lacuna Compendial Calculator Excel was listed under Cat 3 in the README but is authored as a Cat 5 SDS hybrid (Excel + user-developed formula library + named ranges + decision-boundary formulae); Cat 5 list cited 4 systems but is actually 5. Both corrected in README.md.
- **LOW-2: `will` / `should` descriptive usage.** 4 `will` + 3 `should` matches scanned — all descriptive / future-tense / non-normative. No release-blocking fix; no change made.

**Filename rename:** all 50 DS corpus files renamed `*_DS_v1.0.md` → `*_DS_v1.1.md` per § 2B.9 filename version convention. `**Version:**` field in each file's Design Control block bumped from `1.0` to `1.1`. A v1.1 row was appended to every DS Revision History table.

**Verification gates re-run at v1.1:**

- ✅ YAML + disclosures: 50/50 files parse cleanly with valid disclosures
- ✅ Stale-citation grep: 0 hits on forbidden patterns (per § 2A.1–2A.6)
- ✅ Matrix-row range-compression: 0 (Aurora + Hydra + Quartz patched at v1.0; preserved at v1.1)
- ✅ Path resolution: 100% — all 100 `parent_fs.file` + `parent_urs.file` pointers resolve from each DS file's location
- ✅ END marker: 50/50 files
- ✅ Document-number convention: 50/50 match pattern
- ✅ URS-IDs in DS body: 0 (down from 109 at v1.0)
- ✅ Cat 5 SDS files declare EU AI Act Annex classification correctly (Lyrae + Tessera + Hesperia = Annex I 2027; Hydra = per-use-case decision tree; Helios = explicit non-applicability)
- ✅ Tessera Art. 50 transparency coverage added

**Reviewer:** independent quality-review pass by Codex (OpenAI), 25 min wall-clock, 3.77M tokens (3.45M cached). Review report saved at `/tmp/codex-ds-review-2026-05-16.md`.

### v1.0 — initial DS corpus release (2026-05-15)

50 DS files generated via 7 parallel Claude agents, one DS per existing URS+FS pair. Framework files (METHODOLOGY.md, README.md, EVAL_RUBRIC.md) authored before generation. Post-generation patches: Aurora Backup + Hydra GenAI + Quartz AD traceability matrices expanded to per-DS-ID rows (no range compression).
