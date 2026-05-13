# Known Limitations — GAMP 5 Synthetic URS Corpus

We document the limitations of this corpus openly. The goal is to be useful, not to oversell.

## What the corpus does well (v1.2)

- **GAMP-aligned structure** applied consistently across all 50 documents — Purpose, Scope, System Description, User Roles, §5.x by domain (HW / SW / Functional / Part-11 / DI / Backup / Perf / Security / Training / PR / Cross-System Integration), Acceptance, Constraints / Assumptions / Risks, References. URS files end at § 10 References — URS↔FS traceability lives exclusively in FS § 4 + § 8 (per METHODOLOGY § 2A.7 since v1.2).
- **Real specificity, not LLM filler.** Concrete product names (Waters MassLynx 4.2 SCN1027, Acquity I-Class UPLC, Xevo TQ-S micro, Triton / TorchServe / Seldon Core, Veeva Vault, Medidata Rave EDC, Argus Safety, ValGenesis VLM, MES PAS-X, CyberArk PAM, Veeam B&R 12.1, ExaGrid + S3 Object Lock + LTO-9 WORM, etc.) and real numerical anchors (RTO ≤ 8h, RPO ≤ 24h, P95 ≤ 200ms, NTP skew ≤ 1s, krbtgt rotation cadence, NIS2 24h/72h/1-month reporting, Art. 73 15d/10d/2d, FIPS 140-2, AES-256, FIDO2).
- **GAMP categorization done correctly.** Category 4 for configured COTS lab instruments, Category 5 SDLC for custom-developed AI/ML platforms, Category 3 for non-configurable, Category 1 for infrastructure.
- **Every requirement is auditable.** ID + Priority (H/M/L) + GAMP risk class (R1/R2/R3) + a verifiable `shall`-clause a test engineer can sign against. **Traceability lives in the paired FS** (FS § 4 per-ID specification + FS § 8 URS → FS matrix); the URS is FS-namespace-independent.
- **Accurate regulatory citations (v1.2 + v1.1.1 patches).** 21 CFR Part 11 sub-sections .10/.30/.50/.70/.100/.200/.300 (no § 11.55); 21 CFR Part 58 GLP §§ .29/.33/.35/.81/.120/.130/.185/.190/.195; EU Annex 11 §§ 4/4.8/7/7.2/9/11/12; ICH M10 §§ 3/4/3.3.2/4.3.2/3.3.4/4.3.4/5/6.1 (no § 6.1.3/6.4/6.6); ICH E6(R3) Step 4 (adopted 6 Jan 2025); ICH Q1A–Q1E + Q2(R2) + Q3A/B + Q5C + Q9/Q14; PIC/S PI 041-1 (1 July 2021); EU MDR Art. 86 PSUR cadence (Class IIb + III + implantables annual, IIa biennial); FDA CSA for Production and Quality Management System Software (Feb 2026, supersedes Sep 2025); FDA PCCP for AI-Enabled Device Software Functions (Aug 2025); ISPE GAMP 5 2nd ed. (2022); MHRA 2018 DI; FDA DI Q&A 2018; WHO TRS 996 Annex 5 (ALCOA+); EU AI Act 2024/1689 with full Article + Annex map (Annex I = SaMD / safety-component / 2 Aug 2027; Annex III = 8 listed domains / 2 Aug 2026); NIS2 Directive (EU) 2022/2555; GDPR Arts. 30/32/33; ISO/IEC 27001:2022 + Annex A; ISO/IEC 23053 + 23894 + 42001; NIST SP 800-63B / 800-53 Rev.5 / 800-207 / 800-34 / 800-209; FIPS 203/204/205 PQC; ENISA NIS2 guidance; BfR GLP-Bundesstelle + Länder (DE GLP — NOT BfArM); BfArM (DE medicines + devices); Swissmedic (CH); AGES (AT). All citations enforced by METHODOLOGY § 2A.1.
- **`must`/`shall` discipline maintained.** Audit across all 50 URS + 50 FS — every `must` constrains downstream consumers, operators, or quoted regulator text; system requirements use `shall`.
- **Contamination disclaimer is per-document.** Each YAML frontmatter carries `do_not_use_as` containing `regulated_record` and `labelling.source_risk: ai_authored_disclosed`. Dates and identifiers are marked `*(synthetic)*` inline.
- **Cross-system integration wired explicitly (v1.2 Cross-System pass).** Every GxP system in the corpus declares its identity-service integration (AD: Kerberos / LDAPS / SAML / OIDC) and backup-tier participation (RPO/RTO contract). High-value clusters carry deeper bidirectional wiring: AI/ML inference hub (Lyrae) ↔ Tessera CV / RTRT / Watson; GenAI hub (Hydra) ↔ Argus PV / Vault Submissions / EDC; Helios audit-trail ingestion ↔ 13 source systems; eQMS CAPA chain ↔ 10 finding-generators; EDMS SOP / LMS competence bindings across role-bound systems.

## What the corpus does less well

### 1. Length variance across documents — now driven by system tier

v1.2 sizes URS depth by the tier system (METHODOLOGY § 2A.13): T1 instruments (Karl Fischer, particle counter, compendial calculator) at 300–400 L / 30–50 reqs; T2 standard lab+config systems at 400–550 L / 50–80 reqs; T3 enterprise systems (LIMS / ELN / eQMS / EDMS / RIM / RTRT / SCADA / MES / AD) at 600–900 L / 100–150 reqs; T4 mission-critical (EDC, CTMS, eTMF, Vault Submissions, AI/ML Server, GenAI Service, MES PAS-X, PV DB) at 900–1500 L / 150–250 reqs. Variance is deliberate and reflects real-world spec depth.

**Corpus totals (v1.2):** 50 URS = 20,218 lines; 50 FS = 22,479 lines; **42,697 total lines** (vs 21,351 at v1.1.1 — a 2× growth).

**Implication:** if you are training a model on this corpus, sample by tier rather than uniformly across files. If you are using the corpus as a reference template, the tier of your target system tells you which corpus document to lead with.

### 2. Same author voice across all 50

All 50 documents read as if written by the same person. Real-world URS corpora at scale carry noticeable house styles — Roche-house reads differently from Lonza-house, which reads differently from Pfizer-house. The variance dimensions that distinguish house styles (verbosity, table-vs-prose preference, level of vendor-product specificity, German vs English in DACH-context sites, depth of risk treatment) are present but compressed in this corpus.

**Implication:** for fine-tuning, this is probably a feature — you want signal, not noise. For teaching, supplement with side-by-side examples from your own organisation's URS history.

### 3. Implementation Risk Register lives in FS, not URS (v1.3 restructuring)

Since v1.3 (2026-05-13), the URS does NOT carry a "Top-level Risks" section. Implementation / configuration / integration / operational / runtime risks are properties of the *implementation*, not of the *user need* — and have been moved to a new last-numbered-section `## N. Implementation Risk Register` in each paired FS. The URS retains per-requirement GxP-criticality (R1/R2/R3) on every requirement, since that IS a property of the requirement itself (what happens if the user need is not met).

The Implementation Risk Register in each FS currently carries 4–18 entries (T1 minimum; T4 maximum); content was transferred verbatim from the v1.2 URS § 9 tables. **A full formal Risk Assessment (FMEA / HAZOP) remains a separate downstream deliverable** (`<DOC-PREFIX>-RA-NN`, planned for the Day-7 release of the public campaign).

### 4. Company-name diversity is on the cosmic side

Many fictional companies in this batch are named after constellations, Greek figures, and astronomical phenomena (Auriga, Lyrae, Cygnus, Aldebaran, Vela, Aurora, Cassiopeia, Hesper, Crocus, Cithara, Polaris, Solstice, Vesta, Eunoia). This is charming at small scale and templated at 50-doc scale. A planned re-generation pass will mix in grounded fictional names (Müller-Pharma, Nordberg Biotech, Tanaka Therapeutics, Patel Biosciences, Bergland Pharma) to break the pattern.

**Note:** all company names are fictional and the contamination disclaimer holds regardless of name style.

### 5. DACH-specific framing is present but not dominant

Seven documents now (EU MDR PMS DB, Validated GenAI LLM Service, Pharmacovigilance DB, AI/ML Model Server, Watson Bioanalytical LIMS, ValGenesis VLM, ePRO Portal) carry explicit DACH framing — site placements in Germany / Austria / Switzerland with references to BfR GLP-Bundesstelle + Länder (DE GLP authority), BfArM (DE medicines + devices, **not** GLP), Swissmedic (CH), AGES (AT), Fimea (FI), EudraVigilance (EMA), BSI IT-Grundschutz, TISAX, EU AI Act 2024/1689 + EU MDR 2017/745 + NIS2 Directive. The remaining 43 documents lean US/UK / global English. A planned re-generation pass will lift the DACH proportion to ~25% (12–15 documents) to better serve the DACH audience the corpus is aimed at.

### 6. No regulator has signed off on this corpus

This is the most important limitation. The corpus is a *reference* for what GAMP 5 URS look like, generated from public regulatory primary sources. It is not vetted by FDA, EMA, BfArM, Swissmedic, or any other competent authority. The documents themselves are not regulated records and must not be filed, signed, or used as the basis for real validation decisions.

If you intend to derive any operational artefact from this corpus, **a Quality Unit at your organisation must review, edit, sign, and approve it under your site's change control process before it has any regulated status.** That is the line where the corpus stops being useful and your validation engineering takes over.

---

## What v1.2 already delivered (vs v1.1.1)

1. ✅ **All documents now meet tier-target depth** (T1 ≥ 300L / T2 ≥ 400L / T3 ≥ 600L / T4 ≥ 900L) with full §5.x breakout. v1.1 200-line floor has been replaced by tier-driven sizing.
2. ✅ **URS↔FS namespace decoupled** — URS no longer carries Appendix A; FS § 8 is the sole traceability surface. URS can be authored/signed/approved independent of FS namespace evolution.
3. ✅ **EU AI Act re-classification per § 2A.14** — Lyrae AI/ML Model Server, Hydra GenAI Service (use-case-conditional), and Tessera CV all correctly Annex I (2027); Helios audit-trail correctly NOT AI-Act-bound. Full Art. 8–21 / 26 / 43 / 47 / 48 / 49 / 72 / 73 / 99 / 113 coverage on Annex-bound systems.
4. ✅ **Cross-system integration corpus-wide** — 190 new requirements wiring AD identity + Backup tier participation across 48 GxP systems, plus deep cluster wiring for AI inference, GenAI use-cases, Helios audit-trail ingestion, eQMS CAPA chain, EDMS SOP binding, and LMS competence binding.
5. ✅ **Pre-existing v1.0/v1.1 defects fixed inline** — 23 total caught during Waves 1+2+3 (FS-doc-num prefix mismatches, phantom URS-IDs in FS, FS range-compression, missing Part 11 sub-section bindings, namespace mis-mappings).

## What we'd still improve in the next batch (post-v1.2)

1. METHODOLOGY § 2A.1 citation-table consolidator pass — merge the ~140 new authoritative sources surfaced by the 3 enrichment waves into the canonical currency table.
2. Diversify house style across 3–4 voice families (still uniform across 50)
3. Add full RA / FMEA artefacts paired to each URS (Day-7 release)
4. Lift DACH proportion to ~25% (12–15 documents) with explicit DE / FR / IT / NL language re-angles for selected sites
5. Mix grounded fictional company names in to break the cosmic/Greek pattern
6. Add 3–5 deliberately *bad* URS examples with annotated "what's wrong here" commentary, as a training contrast set

## Contact

Open an issue on the GitHub repo or email nat@naitc.de with comments, corrections, or examples of where the corpus reads off-house-style relative to your industry context. The corpus improves with feedback; we'd like to ship a v2 within 60 days of the initial release.
