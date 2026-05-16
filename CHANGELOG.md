# Changelog — GAMP 5 Synthetic URS + FS + DS Corpus

## v1.4 — 2026-05-16 (third specification tier — Design Specifications)

**Released:** 2026-05-16 — extends the corpus from URS + FS pairs to URS / FS / DS triples. Closes the GAMP 5 V-model authoring chain end-to-end for every system in the corpus.

### What's new

- **50 Design Specifications** (`DS/*_DS_v1.1.md`) paired one-to-one with the existing URS + FS by system name. Shape is GAMP-category-driven:
  - **Cat 5 (custom-build)** → full Software Design Specification: module-level decomposition, interface contracts, data models, sequence diagrams, deployment topology, custom-development scope.
  - **Cat 4 (config-on-COTS)** → Configuration Specification: configuration-vs-code split, vendor-feature inventory, environment-scoped configuration items, configuration migration.
  - **Cat 3 (instrument)** → vendor-design-reliance statement + configuration locks.
  - **Cat 1 (infrastructure)** → Infrastructure Design Specification.
- **DS-specific methodology and rubric** ship inside the `DS/` folder (`DS/METHODOLOGY.md`, `DS/EVAL_RUBRIC.md`, `DS/CHANGELOG.md`) — distinct enough from the URS / FS rules that they warranted a dedicated canonical document rather than a new section in the top-level `METHODOLOGY.md`.
- **FS → DS traceability matrix** in every DS, so the URS → FS → DS chain is end-to-end auditable for Cat 4 / Cat 5 systems.
- README + `CITATION.cff` updated to reflect three-tier scope. Badges bumped: files 100 → **150**, lines 42,997 → **79,804**.

### What's *not* in v1.4

- No changes to URS or FS content — both remain at v1.3 file versions.
- Top-level `METHODOLOGY.md` (URS / FS rules) and `EVAL_RUBRIC.md` are unchanged.
- The website hub at https://neuralarchitects.ae/gxp-corpus ships the same v1.4 zip as the GitHub release; both contain all three subtrees.

### Known limitations carried forward

- DS files retain the v1.1 internal version stamp from the SDV-side authoring pipeline; the v1.4 label refers to the *corpus release*, not per-document versions. Future v1.x releases may bump individual DS versions without bumping the corpus version.
- DS Cat 5 modules use illustrative architecture choices; they're not prescriptive for any particular real-world system.

---

## v1.3 — 2026-05-13 (URS structural review — Project Mode + risks-leave-URS)

**Released:** 2026-05-13 — applies the LLM Council verdict (2026-05-13) on three URS structural concerns raised by Nabil Attia. Targeted v1.3 polish, not a rewrite.

### Decisions ratified by LLM Council 2026-05-13

| # | Concern | Council verdict | v1.3 action |
|---|---|---|---|
| Q1 | Vendor naming in Cat 4 URS § 5 (e.g., `Medidata Rave`) | **(C) Hybrid** — vendor naming in scope / vendor-assurance / integrations is legitimate IF the URS is a configuration-on-pre-selected-COTS project; make project mode explicit | New METHODOLOGY § 2A.15 (Project Mode declaration rule) + Project Mode line in every URS Document Control block |
| Q2 | Vendor-named integration sub-sections (Argus, Medidata Coder, Okta, etc.) | **(C) Hybrid** — URS keeps the business-level integration need + named enterprise systems; protocol/endpoint detail moves to FS | Deferred to a future v1.4 polish (no corpus-wide URS rewrites required in v1.3) |
| Q3 | URS § 9 Top-level Risks | **User Option A: remove from URS, move to FS** | New METHODOLOGY § 2A.16 (FS Implementation Risk Register rule). URS § 9 removed corpus-wide; content transferred to FS as a new last-numbered-section Implementation Risk Register. URS § 10 References renumbered to § 9. |

### User-driven rationale for Q3 (recorded for future readers)

> "A requirement is a wish. A wish cannot have risks — only an implementation can fail. The risks in URS § 9 (mid-study amendment defects, integration drift, configuration errors, credential compromise, SAE reconciliation drift) are all implementation / configuration / runtime / operational risks. They belong in FS (where the implementation lives) or in the formal Risk Assessment artefact (FMEA / HAZOP). The per-requirement GxP-criticality column (R1/R2/R3) stays on every URS requirement — that's a property of the wish, not of the implementation."

### Mechanical migration applied (single Python script — `/tmp/v1.3_migrate.py`)

- **All 50 URS** — `**Project Mode:**` line inserted in Document Control block immediately under the `**System Class (GAMP 5, 2nd ed.):**` line. Wording derived deterministically from declared GAMP category (Cat 5 → custom-build; Cat 4 → configuration on commercial software; Cat 3 → configuration on non-configurable instrument; Cat 1 → infrastructure qualification).
- **All 50 URS** — § 9 Top-level Risks section removed entirely. § 10 References renumbered to § 9.
- **All 50 FS** — new last-numbered-section `## N. Implementation Risk Register` appended after the existing URS → FS Traceability Matrix section. Content transferred verbatim from URS § 9 (Risks table) with a new intro paragraph clarifying the implementation-not-wish framing.
- **All 50 FS** — Revision History (top-of-file) table extended with a v1.3 entry documenting the new section.

### METHODOLOGY updates

- **§ 2A.12** Document-structure invariants — URS now declared to end at § 9 References (was § 10). FS now declared to include an Implementation Risk Register as the final numbered section. Rationale paragraph added explaining the wish-vs-implementation framing.
- **§ 2A.15 NEW** Project Mode declaration rule — canonical wordings per GAMP category. Mandatory in every URS Document Control block.
- **§ 2A.16 NEW** FS § 9 Implementation Risk Register rule — placement, structure (`ID | Risk | Likelihood | Impact | Mitigation reference | Implementation surface`), separation from the formal RA artefact.

### Verification — all gates pass (2026-05-13)

- 50/50 URS have Project Mode line directly under System Class
- 50/50 URS no longer carry § 9 Top-level Risks
- 50/50 URS end at § 9 References → END marker
- 50/50 FS now carry an Implementation Risk Register section as last numbered section
- 50/50 FS preserve END marker
- 100/100 files have valid YAML + `do_not_use_as ⊇ {regulated_record}` + `labelling.source_risk = ai_authored_disclosed`
- 0 URS contain Appendix A (preserved from v1.2 decoupling)
- 0 stale-citation hits in actual document content (matches found only in CHANGELOG / METHODOLOGY / README / KNOWN_LIMITATIONS where forbidden patterns are explicitly negated)

### Deferred to v1.4 (post-public-release polish)

- Q2 integration-section refactor — strip protocol/endpoint detail from URS § 5.x integration sub-sections; push to paired FS interface specs
- METHODOLOGY § 2A.1 citation-table consolidator pass — merge ~140 new authoritative citations flagged across Waves 1+2+3
- Final independent regression Codex review

---

## v1.2 — 2026-05-12 (corpus-wide depth enrichment + URS↔FS decoupling + cross-system integration)

**Released:** 2026-05-12 — full v1.2 ships after Waves 1 + 2 + 3 multi-agent enrichment, URS↔FS decoupling (Appendix A removal), and corpus-wide Cross-System integration pass.

**Headline numbers (v1.1.1 → v1.2):**

| Metric | v1.1.1 | v1.2 | Δ |
|---|---|---|---|
| URS files | 50 | 50 | — |
| FS files | 50 | 50 | — |
| URS total lines | 12,111 | **20,218** | +67% |
| FS total lines | 9,240 | **22,479** | +143% |
| **Corpus total lines** | 21,351 | **42,697** | **+100%** |

### v1.2 — Wave 3: AI/Custom (Chunk I) + Infrastructure (Chunk J) + Cross-System pass

**Chunk I — AI / Custom / Cat 5 (4 pairs):**
- `Lyrae_Bioworks AI/ML Model Server` (T4): 306 → 554 L, 150 reqs. **EU AI Act re-classified Annex III (2026) → Annex I (2027)** per § 2A.14 (system serves models embedded in pharmaceutical / SaMD decisions). Added Art. 9/10/11+Annex IV/12/13/14/15/17/18/26/43/47/48/49/72/73/99 coverage + champion/challenger + feature store + drift detection + PCCP envelope + Annex VII conformity pathway.
- `Hydra_BioPharma GenAI LLM Service` (T4): 299 → 590 L, 148 reqs. **Per-use-case classification gate** (Annex I 2027 for GxP-decision-informing / Annex III 2026 for biometric-like / Art. 50 transparency for doc-drafting). Added prompt-injection defense + retrieval grounding + hallucination detection + PII redaction + cost controls + OWASP LLM Top 10 + GPAI obligations Arts. 51–55.
- `Tessera_Bio Custom Computer Vision Inspection` (T3): 255 → 511 L, 129 reqs. **Re-classified Annex I (2027)** (visual inspection of sterile pharmaceutical products = safety component per Annex 1 §8.123 + USP <790>/<1790>). Added camera+lighting qualification, defect-class library with statistical balance, dual-blind labelling protocol with Cohen's κ, Annex 1 challenge-test cadence, retained-human-inspection invariant.
- `Helios_Biosciences Audit Trail Review Workbench` (T3): 322 → 513 L, 111 reqs. **Confirmed NOT AI-Act-bound** (deterministic rule-based, no AI inference) — explicit out-of-scope statement added. Added risk-based + exception-based review prioritisation, MHRA 2018 + FDA DI Q&A 2018 + PIC/S PI 041-1 § 9 bindings, ALCOA+ canonical mapping per WHO TRS 996.

**Chunk J — Infrastructure / IT (2 pairs):**
- `Quartz_Genomics Active Directory Identity Service` (T3): 227 → 601 L, 178 reqs. 22 §5 subsections covering forest/domain architecture (RED forest + RODC), JML lifecycle (Workday-driven, 8h leaver SLA), FIDO2 phishing-resistant authentication, RBAC/ABAC, PAM (CyberArk + Entra PIM + JIT + PAW + break-glass), service accounts (gMSA + workload identity), Kerberos hygiene (krbtgt rotation, AES-only, AS-REP/Kerberoasting defense), Entra ID hybrid, ADCS PKI (offline root + HSM L3 + PQC watch), Part 11 sub-section bindings, NIS2 incident reporting (24h/72h/1-month), GDPR Arts. 30/32/15/17.
- `Aurora_Pharma Backup System for GxP Servers` (T2): 221 → 413 L, 93 reqs. 15 §5 subsections covering 3-2-1-1-0 architecture (ExaGrid + S3 Object Lock + LTO-9 WORM), Oracle RMAN + MS SQL VSS + PostgreSQL pg_basebackup methods, RPO/RTO matrix, Annex 11 § 4.8 + § 7.2 restore-testing cadence (monthly/quarterly/annual + triennial unannounced drill + signed restore certificate ≥25y), ransomware response with clean-room restore, NIS2 reporting.

**Cross-System Pass (190 new reqs corpus-wide):**
- **Tier 1 — universal pairings:** 96 reqs across 48 non-infra URS, wiring every GxP system to AD (Kerberos/LDAPS/SAML/OIDC per system) + Backup (T1/T2/T3 tier with RPO/RTO).
- **Tier 2 — cluster-specific integration:** 94 reqs across selective systems:
  - Lyrae as AI inference hub: Hesperia RTRT (NIR PAT), Watson LIMS bioanalytical, Tessera CV inference
  - Hydra as GenAI hub: Sirius Argus PV triage, Bellerophon Submissions drafting, Marigold EDC protocol drafting
  - Helios audit-trail ingestion: 13 source systems (Empower, RTRT, MES PAS-X, LIMS, ELN, EDMS, EDC, CTMS, eTMF, Submissions, PV, eQMS, ValGenesis)
  - eQMS CAPA chain: 10 finding-generating systems (EU MDR PMS, APR, SPC, Stability, AE DB, Cold Chain, EMS, BMS, ValGenesis, Cleaning Validation)
  - EDMS SOP binding: 4 consumers (LMS, eQMS, Submissions, eTMF)
  - LMS competence binding: 7 role-bound systems (Lyrae, Hydra, Helios, PV, EDC, CTMS, eTMF, MES PAS-X)
  - RTRT/ePRO/MDR data flows verified intact from Wave 1.

**Pre-existing v1.0/v1.1 defects caught + fixed during Wave 3 (8 total):**
- Lyrae FS, Hydra FS, Tessera FS, Helios FS — partial URS-ID namespace mismatch + Tessera FS doc-num prefix bug (TSR→TES) + Tessera FS range-compression (full rewrite)
- Quartz AD FS — full URS-ID namespace mis-mapping (`URS-ID-01..03 / URS-AUTH-01..03` did not exist in URS; re-mapped to actual `URS-ARCH-* / URS-ACC-* / URS-AUTHN-*`)
- Aurora Backup FS — full URS-ID namespace mis-mapping (`URS-POL-* / URS-RST-*` did not exist; re-mapped to actual `URS-COV-* / URS-SCH-* / URS-RPO-* / URS-RTO-* / URS-TEST-*`)
- Vega EU MDR PMS FS — referenced `URS-CFG-03` not present in URS § 5 (added to URS)
- Veridian MES PAS-X FS — `URS-PR-02 → FS-PR-01` collapse (added explicit FS-PR-02 per-ID row)

### v1.2 — Wave 1 + 2 enrichment

50 URS + 50 FS pairs distributed across 10 thematic chunks (A–J); each chunk enriched by a dedicated subagent doing web research per system class and adding tier-appropriate depth (T1 30–50 reqs / T2 50–80 / T3 100–150 / T4 150–250 per METHODOLOGY § 2A.13).

**Wave 1 (Chunks A–D)** — 21 pairs:
- Chunk A (Chromatography + Mass Spec): 5 pairs, avg ~86 reqs (LC-MS, HPLC Empower, ICP-MS, Watson LIMS T3, Hamilton STAR)
- Chunk B (Spectroscopy + Physical-property): 6 pairs, T1–T2, ~72 reqs avg (UV-Vis, NIR, Karl Fischer, TOC, Dissolution, Particle Counter)
- Chunk C (Solid-dose PLCs + MES): 5 pairs, T2–T4, MES PAS-X at T4 floor 151 reqs (Autoclave, Lyophilizer, Tablet Coater, Continuous Mfg, MES PAS-X)
- Chunk D (Bioprocess + SCADA): 5 pairs, T2–T3, ~86 reqs avg (Bioreactor SCADA, Water SCADA, DCS DeltaV, RTRT, EMS)

**Wave 2 (Chunks E–H)** — 23 pairs:
- Chunk E (Enterprise Quality + Docs): 6 pairs, T2–T3, ~88 reqs avg (LIMS, ELN Benchling, EDMS Vault, eQMS MasterControl, CMMS Maximo, ValGenesis VLM)
- Chunk F (Quality Operations): 6 pairs, T1–T3, ~64 reqs avg (APR, Stability ICH Q1A-Q1E, Cleaning Validation HBEL, SPC, Process Historian PI System, Compendial Calculator)
- Chunk G1 (EDC + CTMS T4): 2 pairs, **152 + 150 reqs** (Marigold Medidata Rave EDC, Dryad Veeva Vault CTMS) — fixed pre-existing CTMS URS-ID↔FS-ID mismatch
- Chunk G2 (eTMF + RIM + LMS + ePRO): 4 pairs, T4 + T3 + T2 + T3 (Marinos eTMF DIA-TMFR-3.3.1, Nimbus RIM IDMP, Vega LMS, Iolanthe ePRO uplift)
- Chunk H (PV + Submissions): 5 pairs, T2–T4, **2× T4** (Sirius Argus PV at 150 reqs, EU MDR PMS uplift, Theia Adverse Event, Selene Cold Chain, Bellerophon Veeva Vault Submissions at 150 reqs)

**Pre-existing v1.0/v1.1 defects caught + fixed during Wave 1+2** (15 total):
- 5× FS doc-number prefix mismatches (Chunk B: KST→KSP, IND-KF→IND-CKF, SLA→SOL, SOL-DISS→SOL-DISSO, DRM→DRD)
- 1× CTMS FS referencing phantom URS-IDs not in URS (G1)
- 3× Chunk F FS misalignments (Stability wrong doc-num, Cleaning Cat 5 vs URS Cat 4, SPC NWA vs URS JMP)
- 6× Chunk E FS issues (VLM stale CSA Sep 2025 → Feb 2026, EDMS VLS→VLP doc-num, EDMS+CMMS phantom URS-IDs, ELN+EDMS+CMMS range compression, missing Part 11 sub-section bindings)

### v1.2 — URS Appendix A removed; URS↔FS namespace decoupled

**Decision:** the URS no longer carries Appendix A — Traceability Seed (URS-ID → FS-ID → Test-ID). The URS is now FS-namespace-independent. FS § 8 — URS → FS Traceability Matrix is the SOLE URS↔FS traceability surface in the corpus.

**Rationale:** earlier methodology embedded FS-IDs in URS Appendix A as a forward-planning seed. This created a coupling between the URS (business-owned, stable, higher governance) and the FS namespace (engineering-owned, fluid). FS-ID changes — common during FS-revision cycles (splits, merges, renumberings) — forced URS re-issue with all the higher-tier sign-off that implies. The coupling inverts the intended document hierarchy.

**Trigger:** user observation that the appendix is wordy and forces URS update when FS-IDs change. External LLM-council review (3-0 verdict) confirmed: the 4-places-per-URS-ID pattern is gold-plated relative to GAMP 5 baseline; FS § 8 is the audit-required traceability surface; URS Appendix A duplicates without adding regulatory value.

**Changes applied:**
- `METHODOLOGY.md § 2A.7` rewritten — FS § 4 + § 8 are the sole URS↔FS traceability surfaces; URS Appendix A explicitly forbidden; rationale documented.
- `METHODOLOGY.md § 2A.12` URS structure invariants — § 11 Appendix A removed from required list; URS now ends after § 10 References.
- All 50 URS files — § 11 Appendix A section stripped (mechanical removal); URS files now end with § 10 References → `---` → `**END OF DOCUMENT**` marker.
- Total reduction: **3,355 lines removed across 50 URS** (avg ~67 lines per URS; T4 docs like EDC lost 155+ lines).
- FS files **unchanged** — FS § 4 (per-ID specifications) and FS § 8 (URS → FS traceability matrix) remain the canonical traceability surfaces.

**What this means for downstream users:**
- A URS can now be authored, signed, and approved without any awareness of the FS namespace. FS namespace evolution does not invalidate the URS.
- Traceability auditors look at FS § 8 as the single source of truth.
- The corpus no longer teaches the "URS-IDs appear in 4 places" pattern; it teaches the cleaner "URS owns requirements; FS owns implementation + traceability" separation.

### v1.2.0-rc1 — Wave 1 + 2 enrichment

50 URS + 50 FS pairs distributed across 10 thematic chunks (A–J); each chunk enriched by a dedicated subagent doing web research per system class and adding tier-appropriate depth (T1 30–50 reqs / T2 50–80 / T3 100–150 / T4 150–250 per METHODOLOGY § 2A.13).

**Wave 1 (Chunks A–D)** — 21 pairs:
- Chunk A (Chromatography + Mass Spec): 5 pairs, avg ~86 reqs (LC-MS, HPLC Empower, ICP-MS, Watson LIMS T3, Hamilton STAR)
- Chunk B (Spectroscopy + Physical-property): 6 pairs, T1–T2, ~72 reqs avg (UV-Vis, NIR, Karl Fischer, TOC, Dissolution, Particle Counter)
- Chunk C (Solid-dose PLCs + MES): 5 pairs, T2–T4, MES PAS-X at T4 floor 151 reqs (Autoclave, Lyophilizer, Tablet Coater, Continuous Mfg, MES PAS-X)
- Chunk D (Bioprocess + SCADA): 5 pairs, T2–T3, ~86 reqs avg (Bioreactor SCADA, Water SCADA, DCS DeltaV, RTRT, EMS)

**Wave 2 (Chunks E–H)** — 23 pairs:
- Chunk E (Enterprise Quality + Docs): 6 pairs, T2–T3, ~88 reqs avg (LIMS, ELN Benchling, EDMS Vault, eQMS MasterControl, CMMS Maximo, ValGenesis VLM)
- Chunk F (Quality Operations): 6 pairs, T1–T3, ~64 reqs avg (APR, Stability ICH Q1A-Q1E, Cleaning Validation HBEL, SPC, Process Historian PI System, Compendial Calculator)
- Chunk G1 (EDC + CTMS T4): 2 pairs, **152 + 150 reqs** (Marigold Medidata Rave EDC, Dryad Veeva Vault CTMS) — fixed pre-existing CTMS URS-ID↔FS-ID mismatch
- Chunk G2 (eTMF + RIM + LMS + ePRO): 4 pairs, T4 + T3 + T2 + T3 (Marinos eTMF DIA-TMFR-3.3.1, Nimbus RIM IDMP, Vega LMS, Iolanthe ePRO uplift)
- Chunk H (PV + Submissions): 5 pairs, T2–T4, **2× T4** (Sirius Argus PV at 150 reqs, EU MDR PMS uplift, Theia Adverse Event, Selene Cold Chain, Bellerophon Veeva Vault Submissions at 150 reqs)

**Pre-existing v1.0/v1.1 defects caught + fixed during Wave 1+2** (15 total):
- 5× FS doc-number prefix mismatches (Chunk B: KST→KSP, IND-KF→IND-CKF, SLA→SOL, SOL-DISS→SOL-DISSO, DRM→DRD)
- 1× CTMS FS referencing phantom URS-IDs not in URS (G1)
- 3× Chunk F FS misalignments (Stability wrong doc-num, Cleaning Cat 5 vs URS Cat 4, SPC NWA vs URS JMP)
- 6× Chunk E FS issues (VLM stale CSA Sep 2025 → Feb 2026, EDMS VLS→VLP doc-num, EDMS+CMMS phantom URS-IDs, ELN+EDMS+CMMS range compression, missing Part 11 sub-section bindings)

**Corpus growth (v1.1.1 → post-Wave-2 + Appendix-strip):**
- URS lines: 12,111 → **18,010** (+49% — would be +76% if Appendix A had stayed)
- FS lines: 9,240 → 19,749 (+114%)
- Total: 21,351 → **37,759** lines

**~140 new authoritative citations identified across all 3 waves for METHODOLOGY § 2A.1 expansion** (USP `<>`, Ph. Eur., ICH, EU GVP, IDMP, DIA TMF, SCORM, CDISC, ISO, ISA, IEC, FDA Part 803/314/600, WHO, IMDRF, ASTM, EMA HBEL, ICH Q1A-Q1E + Q5C, WHO TRS, NIST SP 800-63B / 800-53 Rev.5 / 800-207 / 800-34 / 800-209, FIPS 203/204/205 PQC, NIS2 Directive, ISO/IEC 27001:2022 + Annex A, ISO/IEC 23053, ISO/IEC 23894, ISO/IEC 42001, ISO 22301, NIST AI 100-1/600-1, OWASP LLM Top 10, BSI IT-Grundschutz, ENISA NIS2 guidance, EU AI Act 2024/1689 full Article + Annex map per § 2A.14, EU GMP Annex 22 DRAFT, USP <790>/<1790>/<787>/<788>/<1>, Ph. Eur. 2.9.20, PDA TR 79, PIC/S PI 041-1 1 July 2021, FDA GMLP 2021, FDA Inspection of Injectable Products 2021, MHRA 2018 DI Guidance, FDA DI Q&A 2018) — **pending METHODOLOGY § 2A.1 consolidator pass post-v1.2 release.**

### Final verification (v1.2 release gate)

All gates pass on the full 50+50 corpus:
- **YAML + disclosures:** 100/100 files have valid YAML + `do_not_use_as` containing `regulated_record` + `labelling.source_risk: ai_authored_disclosed`
- **URS structure invariants:** 0 URS without § 10 References heading; 0 URS containing Appendix A; 0 URS/FS missing END marker
- **Stale citations:** 0 hits on forbidden patterns (`ICH M10 §§ 6.1.3/6.4/6.6`, `21 CFR § 11.55`, `CSA … September 2025` without supersede note, `BfArM is the GLP authority`, `ICH E6(R3) (2026/revised)`)
- **Pair count:** 50 URS + 50 FS

### Deferred to post-v1.2

- METHODOLOGY § 2A.1 citation-table consolidator pass (~140 new authoritative sources to merge)
- Optional: extend Tier 2 cross-system integration to remaining medium-touch pairings (currently only the high-value clusters are wired; e.g., LMS-competence binding could extend to 5 more role-bound systems)

---

## v1.1.1 — 2026-05-13 (post-review citation + traceability patch)

**Released:** 2026-05-13 — patches v1.1 after an independent quality-review pass surfaced regulatory-citation and traceability defects. The campaign kickoff was postponed by 1 day to allow this patch.

### Critical regulatory-citation fixes

| # | Citation | Before | After | Files affected |
|---|---|---|---|---|
| 1 | FDA CSA | "Computer Software Assurance for Production and Quality System Software (final, September 2025)" | "Computer Software Assurance for Production and **Quality Management** System Software (final, **February 2026**; supersedes September 2025)" | AI/ML URS, GenAI URS, ValGenesis URS+FS, Helios URS, Tessera URS, README |
| 2 | FDA PCCP | "Marketing Submission Recommendations for a Predetermined Change Control Plan for AI/ML-Based Device Software Functions (2024)" | "Marketing Submission Recommendations for a Predetermined Change Control Plan for **Artificial Intelligence-Enabled** Device Software Functions (**August 2025**)" | AI/ML URS+FS, GenAI URS+FS, README, KNOWN_LIMITATIONS |
| 3 | ICH M10 sections | "§ 6.1.3 (run acceptance), § 6.4 (reanalysis), § 6.6 (ISR)" — sections that don't exist | "§§ 3.3.2 / 4.3.2 (run acceptance), §§ 3.3.4 / 4.3.4 (reanalysis), § 5 (ISR), § 6.1 (partial validation)" | Watson URS+FS |
| 4 | ICH E6(R3) | "ICH E6(R3) GCP (2026 revised version)" | "ICH E6(R3) GCP (**Step 4, adopted 6 January 2025**)" | ePRO URS+FS, Watson URS+FS |
| 5 | EU MDR PSUR cadence | "Class III + implantables annually; otherwise every 2 years" — omits Class IIb | "**Class IIb + Class III + implantables annually**; **Class IIa biennial**; Class I uses PMSR per Art. 85" | EU MDR PMS URS+FS |
| 6 | 21 CFR § 58.33(b) | Bound to Principal Investigator role (false — PI is not CFR-defined) | PI reframed as multi-site GLP convention per OECD; § 58.33(b) reference dropped | Watson URS |
| 7 | BfArM GLP authority | "BfArM (DE) is the GLP inspecting authority" (false) | **BfR GLP-Bundesstelle + Länder authorities** for German GLP monitoring (BfArM covers medicines + devices, not GLP) | Watson URS+FS |

### URS↔FS traceability rebuild

5 of 7 v1.1 paired FS docs used compressed range notation (`URS-PART11-01..07 → FS-PART11-01..07`) violating the per-ID traceability rule in METHODOLOGY § 2A.7. v1.1.1 expands all compressed ranges into explicit per-ID rows in both FS § 4 (Functional Specifications) and FS § 8 (Appendix A — Traceability Matrix). Per-ID specifications were also differentiated for Part-11, ALCOA+/DI, and GLP rows so each FS-ID has a unique implementation statement.

**Coverage at v1.1.1:** 100% URS-ID coverage in paired FS across all 7 v1.1 pairs (verified by `extract_ids` script in verification sweep).

### YAML frontmatter fixes

- `Validation_Lifecycle_Management_ValGenesis__Cygnus_Pharma_URS_v1.3.md`: line 11 `seed_corpus_basis` entries with `:` separators quoted into block-style list.
- `Vega_Devices_PMS_DB_FS_v1.3.md`: lines 4-5 quoted generator string and converted inline flow-style list to block-style with quoted entries (em-dashes + colons + semicolons need quoting).

**Coverage at v1.1.1:** 100/100 corpus files parse cleanly with valid disclosures (`do_not_use_as: regulated_record` + `labelling.source_risk: ai_authored_disclosed`).

### `shall` / `must` discipline fix

- `Custom_Computer_Vision_Inspection_System__Tessera_Bio_URS_v1.3.md` URS-ML-03: `must` → `shall` (system-requirement line, not consumer-constraint).

**Coverage at v1.1.1:** 4 `must` occurrences across 50 URS, all verified as downstream-consumer or process constraints (per METHODOLOGY § 2A.8).

### METHODOLOGY expansion

Added § 2A "Citation Rules and URS/FS Authoring Conventions" — the canonical rule-set encoding the lessons from this review. Twelve sub-sections (§ 2A.1 through § 2A.12) cover:

- § 2A.1 Citation currency reference table (FDA / EU / ICH / DACH titles + dates as of 2026-05-13)
- § 2A.2 21 CFR Part 11 sub-section authority map
- § 2A.3 ICH M10 section numbering — chromatographic vs LBA
- § 2A.4 EU MDR PSUR cadence rule per device class
- § 2A.5 21 CFR Part 58 GLP role rules
- § 2A.6 DACH authority assignment matrix (BfArM ≠ GLP)
- § 2A.7 URS-ID → FS-ID 1-to-1 explicit-row traceability rule
- § 2A.8 `shall` / `must` discipline
- § 2A.9 YAML frontmatter syntax rules
- § 2A.10 GAMP-category-coherence rule
- § 2A.11 EU AI Act high-risk-AI obligations checklist
- § 2A.12 Document-structure invariants

Plus new § 7 "Review history" documenting the v1.1.1 review pass + corrections.

### Verification at v1.1.1 release

All six post-generation validation checks (§ 1.2 Stage 6 of METHODOLOGY) pass:

- ✅ `shall` / `must` lint — clean
- ✅ Citation accuracy — all citations match § 2A.1 current-versions table
- ✅ GAMP-category coherence — all 7 v1.1 URS match declared category structure
- ✅ Traceability — 100% URS-ID coverage in paired FS for all 7 v1.1 pairs
- ✅ YAML frontmatter — 100/100 files parse with valid disclosures
- ✅ Length sanity — all 50 URS ≥ 150 lines; median 196

---

## v1.1 — 2026-05-11 (pre-Day-0 enrichment pass)

**Released:** 2026-05-12 (Wed) — postponed from 2026-05-12 (Tue) per § 4 of campaign strategy to allow this enrichment pass.

### Added — corpus metadata

- **`METHODOLOGY.md`** — full generation-pipeline documentation, regulatory-grounding mechanism, contamination guarantee, license posture
- **`EVAL_RUBRIC.md`** — 6-dimension human-QA reviewer rubric for Day-30 model evaluation
- **`CHANGELOG.md`** — this file
- **`CITATION.cff`** — machine-readable citation metadata
- **`README.md`** — updated coverage + structure description
- **`KNOWN_LIMITATIONS.md`** — honest limitations + v1.2 roadmap

### Hand-expanded — 7 priority URS (all originally-collapsed docs)

These documents received a full §5 breakout (collapsed `§5.x Audit / Part 11 / DI / ...` split into 11–13 separate subsections), DACH-context site relocation, framework-specific regulatory binding, expanded References organised by jurisdiction, and 10–12-row risk tables:

| Document | Before | After | DACH site | Key framework additions |
|---|---|---|---|---|
| `AI_ML_Model_Server_GxP__Lyrae_Bioworks_URS_v1.3.md` | 152 L, 4 §5 subsections | **342 L**, 13 §5 subsections | München (DE) | EU AI Act 2024/1689 Arts. 9–17; Human Oversight Operator role; PCCP per FDA Aug 2025; model-poisoning + Art. 15 cybersecurity; BfArM + Swissmedic + AGES gateways |
| `Validated_GenAI_LLM_Service_GxP__Hydra_BioPharma_URS_v1.3.md` | 156 L, 5 §5 subsections | **332 L**, 13 §5 subsections | Basel (CH) | EU AI Act per-use-case classification; vendor LLM management (Anthropic / OpenAI); GDPR Arts. 22 + 35 DPIA; prompt-injection defences |
| `EU_MDR_Post_Market_Surveillance_DB__Vega_Devices_URS_v1.3.md` | 156 L, 6 §5 subsections | **329 L**, 13 §5 subsections | Tuttlingen (DE medtech hub) | EU MDR Articles 83–92 coverage (PMS Plan, PSUR, Art. 87 incident, Art. 88 trend, Art. 89 FSCA); TÜV SÜD CE 0123; ISO 14971:2019; BfArM / Swissmedic / AGES national CA gateways |
| `Real_Time_Release_Testing_Platform__Hesperia_BioPharma_URS_v1.3.md` | 173 L, 4 §5 subsections | **318 L**, 11 §5 subsections | Visp (CH) | Qualified Person override authority (Directive 2001/83/EC Art. 51); ICH Q12 Established Conditions; ICH Q13 continuous manufacturing; determinism verification |
| `ePRO_Patient_Portal__Iolanthe_Clinical_URS_v1.3.md` | 178 L, 6 §5 subsections | **332 L**, 12 §5 subsections | Wien (AT) | ICH E6(R3) GCP (Step 4, adopted 6 January 2025); EU CTR 536/2014 + CTIS; GDPR Arts. 6, 9, 22, 32, 35 DPIA; BfArM + PEI + Swissmedic + AGES; DACH language variants (de-DE, de-AT, de-CH); ICH E6(R3) §3.10 RBM |
| `Validation_Lifecycle_Management_ValGenesis__Cygnus_Pharma_URS_v1.3.md` | 170 L, 5 §5 subsections | **332 L**, 12 §5 subsections | Konstanz (DE) | FDA CSA (Sep 2025) risk-based-testing classification; ICH Q9(R1) risk classification with critical-thinking justification; Annex 11 §§ 4, 6, 9, 11 explicit; BfArM Anlage 7; recursive validation-of-validation framing |
| `Watson_LIMS_Bioanalytical__Cetus_Pharmacology_URS_v1.3.md` | 167 L, 4 §5 subsections | **330 L**, 12 §5 subsections | Heidelberg (DE) | ICH M10 acceptance criteria (calibrators ± 15%, QCs ± 15%, ISR ± 20%); 21 CFR Part 58 GLP sub-section bindings (§§ .29, .33, .35, .81, .120, .130, .185, .190, .195); Study Director + Principal Investigator + QAU role separation; OECD GLP |

### FS catch-up — 7 priority FS

All FS docs paired to v1.1-expanded URS were re-expanded to v1.1 with implementation detail for every new URS-ID, ensuring 1-to-1 URS↔FS traceability:

| FS document | Before | After | Implementation focus |
|---|---|---|---|
| `Lyrae_Bioworks_AI_ML_Model_Server_FS_v1.3.md` | ~110 L | ~290 L | EU AI Act Arts. 9–17 implementations: Sigstore signing, kube-bench CIS, HashiCorp Vault, Splunk frozen-index, Human Oversight UI, PCCP predicate engine |
| `Hydra_BioPharma_GenAI_LLM_Service_FS_v1.3.md` | ~115 L | ~290 L | EU AI Act per-use-case + vendor LLM mgmt: 4-of-4 approval verifier, Microsoft Presidio + NLI hallucination detector, Lakera prompt-injection defence, DPIA registry |
| `Vega_Devices_PMS_DB_FS_v1.3.md` | ~113 L | ~280 L | EU MDR Arts. 87/88/89 + national CA gateways: BfArM/Swissmedic/AGES routing, MDCG-compliant Art. 88 trend generator, FSN template engine |
| `Hesperia_BioPharma_RTRT_FS_v1.3.md` | ~117 L | ~270 L | ICH Q12 EC-classification engine, determinism verification (decimal + IEEE-754 round-mode pin), QP signature gateway, variation-tracking gate |
| `Iolanthe_Clinical_ePRO_Patient_Portal_FS_v1.3.md` | ~120 L | ~270 L | ICH E6(R3) + EU CTR / CTIS integration, DACH language variants (de-DE/de-AT/de-CH), GDPR Arts. 22/35, RBM data feed |
| `Cygnus_Pharma_ValGenesis_VLM_FS_v1.3.md` | ~119 L | ~250 L | FDA CSA (2025) risk-classification engine, ICH Q9(R1) justification capture, evidence-hash verification, RTM-completeness gate with risk-justified exemptions |
| `Cetus_Pharmacology_Watson_LIMS_FS_v1.3.md` | ~114 L | ~270 L | ICH M10 acceptance engine, 21 CFR Part 58 GLP role separation (Study Director + PI + QAU), Archivist-only archive gateway, inspection-readiness export |

### Programmatic upgrades — 42 URS

A mechanical, content-preserving script upgraded the §7 *Constraints / Assumptions / Risks* combined section into three properly-numbered sections across 42 URS documents:

- **§7 Constraints** (was inline bullet)
- **§8 Assumptions** (was inline bullet)
- **§9 Top-level Risks** — now a 5-column table (`ID | Risk | Likelihood | Impact | Mitigation reference`) with heuristically-assigned likelihood + impact, content preserved from the original semicolon-separated risk list

This bumped subsequent section numbers (References, Appendix A) by 2.

**Why mechanical?** The original bullet-format risks were per-doc-specific and accurate. The script preserves the content verbatim while reformatting for visual + audit consistency. No new risks were synthesised — the heuristic only assigns Likelihood/Impact columns based on keyword inspection of the existing risk text.

### Skipped — documented for v1.2

The following improvements were scoped out of v1.1 due to session-budget constraints and risk of introducing regulatory inaccuracy under time pressure:

- **All originally-collapsed URS now expanded.** The detection script identified 7 docs with collapsed `§5.x Audit / Part 11 / DI / ...` sections; all 7 have been hand-expanded with full §5 breakouts, DACH relocation, and framework-specific bindings. (Note: `Pharmacovigilance_Safety_Database` was on the original list but a closer review showed it already had 12 well-structured §5 subsections — false positive on the collapsed-detection regex.)
- **FS file matching expansions: COMPLETED in v1.1.** All 7 FS docs paired to v1.1-expanded URS were re-expanded with implementation detail for every new URS-ID: `Lyrae_Bioworks_AI_ML_Model_Server_FS`, `Hydra_BioPharma_GenAI_LLM_Service_FS`, `Vega_Devices_PMS_DB_FS`, `Hesperia_BioPharma_RTRT_FS`, `Iolanthe_Clinical_ePRO_Patient_Portal_FS`, `Cygnus_Pharma_ValGenesis_VLM_FS`, `Cetus_Pharmacology_Watson_LIMS_FS`. URS↔FS line-by-line traceability fully restored at v1.1.
- **DACH-proportion lift to 25%:** 7 of 50 URS are now DACH-flavored (14%). v1.2 will lift to 12–15 DACH-context docs.
- **Cosmic-naming diversification:** acknowledged in KNOWN_LIMITATIONS § 4; deferred to v1.2.
- **Day-7 Risk Assessment artefacts:** per campaign strategy, RA docs ship separately on Day 7.

### Quality posture

- **`must`/`shall` discipline:** spot-check at v1.1 release found 10 occurrences of `must`, all verified correct (constrain downstream consumers / processes, not the system).
- **Regulatory-citation accuracy:** all citations in the 2 hand-expanded docs verified against current regulatory sources; all citations in the 42 programmatically-upgraded docs preserved from v1.0 (which passed the v1.0 citation-accuracy check).
- **Traceability seed coverage:** preserved or expanded in all 50 URS.

---

## v1.0 — 2026-04-26 to 2026-04-28 (initial generation)

Initial generation of 153 URS + 137 FS in `_generated/`. Curation to top 50 URS↔FS pairs by combined length, with paired-doc consistency verified.

### Coverage

50 systems across GAMP Categories 1, 3, 4, 5 — lab instruments, production control, enterprise quality applications, infrastructure, custom-developed AI/ML platforms.

### Disclosure

Per-document YAML frontmatter with `do_not_use_as: regulated_record` and `source_risk: ai_authored_disclosed`. Inline `*(synthetic)*` markers on dates and personnel placeholders.
