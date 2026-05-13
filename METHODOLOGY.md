# Methodology — How This Corpus Was Built

**Audience:** Quality Assurance leads, validation engineers, and IT compliance professionals in DACH pharma / biotech / medical-device organisations who need to know the provenance, regulatory grounding, and contamination posture of this corpus before considering it for any internal use.

**TL;DR.** The corpus was generated from publicly-available regulatory primary sources only — never from any client URS, never from scraped or anonymised customer data. Each document is structurally constrained to the ISPE GAMP 5 (2nd Ed., 2022) canonical skeleton, regulatorily anchored to FDA, EMA, ICH, PIC/S, and EU AI Act primary text, and disclosed in machine-readable frontmatter as `ai_authored_disclosed` with `do_not_use_as: regulated_record`. The generation pipeline is open-source and is published alongside the corpus.

---

## 1. Generation pipeline

### 1.1 Architecture

```
                  ┌──────────────────────────────────┐
                  │  Regulatory primary-source pack  │
                  │  (read-only inputs to generator) │
                  └──────────────┬───────────────────┘
                                 │
        ┌────────────────────────┼────────────────────────┐
        │                        │                        │
        ▼                        ▼                        ▼
┌──────────────┐        ┌──────────────────┐    ┌───────────────────┐
│ FDA / CFR /  │        │ ISPE GAMP 5      │    │ EU GMP / Annex 11 │
│ CSA / AI-ML  │        │ (2nd Ed., 2022)  │    │ EU AI Act 1689    │
│ Action Plan  │        │ + GPGs           │    │ + Eudralex Vol 4  │
│ + PCCP       │        │                  │    │ + EU MDR / IVDR   │
└──────┬───────┘        └────────┬─────────┘    └───────┬───────────┘
       │                         │                      │
       └─────────────────────────┼──────────────────────┘
                                 │
                    ┌────────────▼─────────────┐
                    │  System catalogue        │
                    │  (153 system archetypes  │
                    │   × intended-use frames) │
                    └────────────┬─────────────┘
                                 │
                                 ▼
                ┌──────────────────────────────────┐
                │  Generator (LLM)                  │
                │  + structural template prompt     │
                │  + per-system context pack        │
                │  + GAMP 5 conventions invariants  │
                │  + per-document originality seed  │
                └────────────┬─────────────────────┘
                             │
                             ▼
                ┌──────────────────────────────┐
                │  Per-document YAML frontmatter │
                │  Per-document body            │
                │  Per-document traceability seed│
                │  Per-document disclosure block │
                └────────────┬─────────────────┘
                             │
                             ▼
                ┌──────────────────────────────┐
                │  Post-generation validation   │
                │  - shall/must lint            │
                │  - citation accuracy check    │
                │  - GAMP-category coherence    │
                │  - traceability seed coverage │
                │  - YAML frontmatter present   │
                │  - length sanity              │
                └────────────┬─────────────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │  /final — 50+50      │
                  │  curated batch       │
                  └──────────────────────┘
```

### 1.2 Pipeline stages

**Stage 1 — Regulatory primary-source pack** (one-time, version-controlled).
A read-only directory holds canonical text from FDA, EMA, ICH, ISPE GAMP 5 (2nd Ed., 2022), PIC/S PI 041, EU GMP Annex 11, EU AI Act 2024/1689, EudraLex Vol 4, EU MDR 2017/745, EU IVDR 2017/746, ISO 13485:2016, ISO/IEC 27001:2022. These are publicly available regulatory documents — not customer documents, not internal client URS. Each source file in the pack carries: title, jurisdiction, version/edition, publication date, official URL, retrieval date, and SHA-256 hash. The hashes are committed to git so any contributor can verify the pack against the published source.

**Stage 2 — System catalogue.**
A catalogue of 153 GxP-regulated system archetypes covering lab instruments, production control systems, enterprise quality applications, infrastructure, and custom-developed AI/ML platforms. Each entry carries: system type, GAMP category target (1/3/4/5), intended-use frame, typical vendor product family (where COTS), and the regulatory frameworks that bind it. The catalogue is curated, not generated — it is the engineer's plan of what to write.

**Stage 3 — Per-document context pack.**
For each document in the run, the pipeline assembles a context pack: the system-catalogue entry, the matching regulatory subset (e.g., "Cat 4 lab instrument → 21 CFR § 11.10/.30/.50, EU Annex 11 sections 4/5/9/12, PIC/S PI 041, ICH Q2(R2)"), and a structural-template prompt enforcing the GAMP-aligned skeleton (§§ 1–11 + Appendix A — Traceability Seed).

**Stage 4 — Generation invariants** (encoded in the prompt).
Hard rules the generator must obey:

- Every requirement carries `(ID, Priority H/M/L, GAMP risk R1/R2/R3, shall-clause)`
- `shall` is the normative verb for system-requirement lines; `must` is reserved for constraints on downstream consumers or processes
- GAMP category, when assigned, must drive the validation depth and the structure of §5
- Per-document electronic-signature, ALCOA+, and audit-trail sections must cite the specific 21 CFR § 11 sub-section (`.10` / `.30` / `.50` / `.70` / `.100` / `.200` / `.300`) being implemented — never a generic "21 CFR Part 11"
- Vendor product names and version strings, when used, must reference a real publicly-documented product (e.g., Waters MassLynx 4.2 SCN1027, Marchesini Integra 720, Waters Acquity I-Class UPLC). The pipeline does not fabricate vendor product names.
- Acceptance Criteria (§ 6) must list the named validation deliverables that gate go-live (FS, CS, RA, IQ, OQ, PQ, VSR, RTM) in the order GAMP 5 prescribes
- Every requirement must have at least one entry in Appendix A — Traceability Seed referencing its planned FS-ID and IQ/OQ/PQ test
- Each document must declare a `do_not_use_as: regulated_record` flag in its YAML frontmatter
- The frontmatter must include the generator identity, the generation date, and the seed-corpus basis

**Stage 5 — Per-document originality seed.**
A short list of variations the generator is asked to apply per-document (e.g., site location, fictional company name, fictional document number prefix, fictional process owner role) to differentiate documents while preserving the regulatory backbone.

**Stage 6 — Post-generation validation.**
Automated checks run on every generated document:

| Check | What it verifies |
|---|---|
| `shall`/`must` lint | `shall` is the normative verb; flag `must` occurrences outside quoted regulator text |
| Citation accuracy check | Every regulator citation in § 10 (References) resolves to a real, currently-effective regulatory document — no hallucinated guidances, draft documents flagged as draft |
| GAMP-category coherence | If the document declares Cat 4, § 5 must include `Software Configuration Requirements`. If Cat 5, § 5 must include `Custom Development Lifecycle`. Cat 1 documents must not carry IQ/OQ/PQ in their acceptance criteria — they qualify infrastructure differently |
| Traceability seed coverage | Every URS-ID in § 5 must appear in Appendix A → planned FS-ID + planned test-ID |
| YAML frontmatter present | The disclosure block must be parseable and contain the seven labelling fields (artifact_class, artifact_status, generator, seed_corpus_basis, do_not_use_as, intended_use, labelling.*) |
| Length sanity | Documents below the 150-line floor are flagged for re-generation or excluded from the curated batch |
| Cross-document consistency | Within a URS↔FS pair, every URS-ID referenced in § 5 of the URS must have a matching FS-ID in § 5 of the FS with the same numeric suffix |

The `/final` curated batch passed all six checks at v1.1.1 release (2026-05-13), after corrections from an external review pass (see § 7.2 Review history). Prior to v1.1.1, several v1.1 documents carried citation defects that have since been fixed; the v1.1.1 release is the first to satisfy all six checks simultaneously across the 7 hand-expanded URS+FS pairs.

### 1.3 Reproducibility

The pipeline is open-source and licensed under **Apache 2.0** (consistent with the model license — see § 5). The repository structure:

```
gamp5-corpus/
├── generator/
│   ├── prompts/                  ← the GAMP-5-anchored structural templates
│   ├── regulatory_source_pack/   ← read-only, hash-pinned regulatory primary sources
│   ├── system_catalogue.yaml     ← 153 system archetypes with category + framework binding
│   ├── invariants.md             ← the hard rules the generator must obey
│   └── validate.py               ← post-generation validation checks
├── URS/                          ← published URS dataset
├── FS_FDS/                       ← published FS dataset
├── docs/
│   ├── METHODOLOGY.md            ← this file
│   ├── KNOWN_LIMITATIONS.md
│   └── EVAL_RUBRIC.md            ← the Day-30 human-QA reviewer rubric
├── LICENSE                       ← CC-BY-SA 4.0 for the dataset
├── LICENSE-CODE                  ← Apache 2.0 for the generator + scripts
├── CITATION.cff
└── CONTRIBUTING.md
```

Anyone with access to the generator, the regulatory source pack hashes, and the system catalogue can re-generate a corpus of the same shape (though not bit-identical — LLM sampling is stochastic). The system catalogue + invariants + prompts define the *shape* of the corpus, and the regulatory pack defines the *grounding* — that is the reproducibility contract.

---

## 2. Regulatory grounding

The corpus is generated against publicly-available regulatory primary sources. Each document's § 10 (References) lists the specific framework citations that bind the system being specified.

### 2.1 The regulatory frameworks the corpus is anchored to

**US — Food and Drug Administration:**
- 21 CFR Part 11 — Electronic Records; Electronic Signatures (§§ .10, .30, .50, .70, .100, .200, .300)
- 21 CFR Part 211 — Current Good Manufacturing Practice for Finished Pharmaceuticals (§§ .22, .68, .180, .192)
- 21 CFR Part 820 — Quality System Regulation for Medical Devices (§§ .30, .40, .70, .80, .90)
- FDA Computer Software Assurance for Production and Quality Management System Software (final guidance, February 2026; supersedes the September 2025 guidance)
- FDA Guidance on AI/ML-Based Software as a Medical Device, Action Plan (2021)
- FDA Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions (August 2025)
- FDA Guidance on Data Integrity and Compliance with cGMP (2018)

**EU — European Medicines Agency / European Commission:**
- EU GMP Annex 11 — Computerised Systems (operational since 2011)
- EU GMP Annex 22 — Artificial Intelligence (DRAFT, consultation closed October 2025 — marked as draft in any document that cites it)
- EudraLex Volume 4 — Good Manufacturing Practice (Parts I + II + III)
- EU MDR 2017/745 — Medical Device Regulation
- EU IVDR 2017/746 — In Vitro Diagnostic Regulation
- EU AI Act 2024/1689 — high-risk AI obligations Articles 9 (risk management), 10 (data governance), 12 (technical documentation), 13 (transparency), 14 (human oversight), 15 (accuracy + robustness + cybersecurity), 17 (quality management system). EU AI Act deadline for high-risk AI systems: **2 August 2026** (~12 weeks from this corpus's release).
- EMA Q&A on Annex 11

**International — ICH:**
- ICH Q2(R2) — Validation of Analytical Procedures
- ICH Q3A(R2) — Impurities in New Drug Substances
- ICH Q3B(R2) — Impurities in New Drug Products
- ICH Q9(R1) — Quality Risk Management
- ICH Q10 — Pharmaceutical Quality System
- ICH Q14 — Analytical Procedure Development

**Industry guidance — ISPE / PIC/S / ISO:**
- ISPE GAMP 5 (2nd Edition, 2022) — the canonical structural reference
- ISPE GAMP Good Practice Guide: AI/ML in GxP (2024)
- ISPE GAMP Good Practice Guide: Records and Data Integrity
- ISPE GAMP Good Practice Guide: Validation of Laboratory Computerized Systems
- PIC/S PI 041 — Good Practices for Data Management and Integrity in Regulated GMP/GDP Environments
- ISO 13485:2016 — Medical Devices: Quality Management Systems
- ISO/IEC 27001:2022 — Information Security Management Systems

**DACH-specific (referenced in DACH-flavored documents):**
- **BfArM (DE)** — Bundesinstitut für Arzneimittel und Medizinprodukte — covers **medicinal products + medical devices** (NOT GLP — see § 2A.6).
- **Paul-Ehrlich-Institut (DE)** — federal authority for biological medicinal products + vaccines.
- **BfR (DE) GLP-Bundesstelle** — Federal Bureau for Good Laboratory Practice at the Bundesinstitut für Risikobewertung, organising GLP monitoring with **Länder (state) authorities**. This is the authority for GLP, not BfArM.
- **Swissmedic (CH)** — Swiss Agency for Therapeutic Products.
- **AGES PharmMed (AT)** — Österreichische Agentur für Gesundheit und Ernährungssicherheit.
- **Anlage 7 GMP-Inspektion (DE)** — German GMP inspection annex.
- **EudraVigilance** — EU pharmacovigilance database (EMA-operated).
- **CTIS** — Clinical Trials Information System (EU CTR 536/2014 submission portal).
- German MPG (Medizinproduktegesetz) — superseded by EU MDR + MPDG (Medizinprodukterecht-Durchführungsgesetz); cited only for historical context.

### 2.2 How regulatory grounding is enforced

Three mechanisms together:

**(a) Hash-pinned regulatory source pack.** The corpus generator reads from a read-only, SHA-256-hash-pinned directory of regulatory primary-source text. The hashes are committed to git. Any contributor can verify the source pack against the published regulatory documents — the contract is that the corpus's regulatory anchoring traces back to *these specific source files at these specific versions*.

**(b) Per-system framework binding.** The system catalogue maps each archetype to its bound regulatory subset. A Cat 4 lab instrument binds to 21 CFR Part 11 + Annex 11 + relevant ICH + PIC/S PI 041. A Cat 5 AI/ML platform binds to those plus GAMP GPG AI/ML, FDA AI/ML Action Plan, EU AI Act 1689 Articles 9–17. An EU MDR Post-Market Surveillance system binds to EU MDR 2017/745 + ISO 14971 + relevant EU MEDDEV documents. The binding is curated by an engineer and reviewed before generation runs — it is not LLM-decided at generation time.

**(c) Post-generation citation check.** Every regulatory citation in § 10 (References) of every generated document is checked against a maintained list of known-real regulatory documents. The check catches three failure modes: hallucinated guidances ("FDA Guidance on Quantum Validation" — a known LLM failure mode), version drift ("21 CFR Part 11 (1995 edition)" — the year is wrong), and section-number errors ("21 CFR § 11.55" — Part 11 has no § .55).

### 2.3 What the regulatory grounding does NOT do

- It does **not** make the corpus a regulated record. Regulatory grounding establishes that the corpus's *structure and references* align with the framework. The corpus is still synthetic and disclosed as such.
- It does **not** replace the Quality Unit's review of any derivative artefact. If you produce a real URS from this corpus's template, your Quality Unit's review under your site's change control is what makes it a regulated record.
- It does **not** mean every requirement statement in the corpus is the right requirement for your system. The corpus is a *reference shape*, not a prescription.

---

## 2A. Citation Rules and URS/FS Authoring Conventions

This section is the **canonical rule-set** for how to cite regulatory documents and how to structure URS+FS in this corpus. Encoded from external review findings (see § 7.2 Review history). Every rule here is enforced in the post-generation validation pass of § 1.2 Stage 6.

### 2A.1 Citation currency — the canonical reference table

Regulatory guidance documents get superseded. Citing a guidance by its old date is a credibility hit. This table lists the **current effective** version of every regulatory document the corpus cites, as of the v1.1.1 release date (2026-05-13). Re-verify at each generation run.

| Authority | Document | Cite as | Notes |
|---|---|---|---|
| FDA | Computer Software Assurance | "FDA *Computer Software Assurance for Production and Quality **Management** System Software* (final, February 2026; supersedes the September 2025 guidance)" | Title contains "Management" (Quality Management System Software). Feb 2026 supersedes Sep 2025. |
| FDA | PCCP for AI-Enabled Devices | "FDA *Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions* (August 2025)" | Title is "Artificial Intelligence-Enabled" (not "AI/ML-Based"). Aug 2025 supersedes the 2024 draft. |
| FDA | AI/ML SaMD Action Plan | "FDA *Artificial Intelligence/Machine Learning–Based Software as a Medical Device Action Plan* (2021)" | Still current. |
| FDA | 21 CFR Part 11 | "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300" | Only these sub-sections exist. Anything else is a hallucination. |
| FDA | 21 CFR Part 58 (GLP) | "21 CFR Part 58 §§ .29, .33, .35, .81, .120, .130, .185, .190, .195" | Sub-sections that exist; cite specifically. |
| FDA | 21 CFR Part 211 (CGMP) | "21 CFR Part 211 §§ .22, .68, .180, .192" | |
| FDA | 21 CFR Part 820 (QSR) | "21 CFR Part 820 §§ .30, .40, .70, .80, .90, .100, .198" | |
| EU Commission | EU AI Act 2024/1689 | "EU AI Act 2024/1689 Arts. 6, 9–17, 50, 72, 73 (high-risk + transparency + post-market)" | High-risk-AI deadline: **2 August 2026**. |
| EU Commission | EU MDR 2017/745 | "EU MDR Reg. 2017/745 Arts. 83 (PMS), 84 (PMS Plan), 85 (PMS Report / PSMR), 86 (PSUR), 87 (Serious incidents), 88 (Trend reporting), 89 (FSCA), 92 (EUDAMED)" | See § 2A.4 for PSUR cadence. |
| EU EMA | EU GMP Annex 11 | "EU GMP Annex 11 §§ 4 (validation), 6 (accuracy), 9 (audit trail), 11 (periodic evaluation)" | |
| EU EMA | EMA AI Reflection Paper | "EMA *Reflection Paper on the use of Artificial Intelligence in the Medicinal Product Lifecycle* (2024)" | |
| ICH | E6(R3) GCP | "ICH E6(R3) — Good Clinical Practice (Step 4, adopted **6 January 2025**)" | Do NOT cite as "2026 revised" — that designation does not exist. |
| ICH | M10 Bioanalytical Method Validation | "ICH M10 — Bioanalytical Method Validation and Study Sample Analysis (Step 4, 24 May 2022)" | See § 2A.3 for section numbering. |
| ICH | Q9(R1) | "ICH Q9(R1) — Quality Risk Management" | |
| ICH | Q12 | "ICH Q12 — Technical and Regulatory Considerations for Pharmaceutical Product Lifecycle Management" | See § 2A.5 for Established Conditions. |
| ICH | Q13 | "ICH Q13 — Continuous Manufacturing of Drug Substances and Drug Products (FDA implementing guidance, 2024)" | |
| Directive | 2001/83/EC | "Directive 2001/83/EC Art. 51 (QP — Qualified Person batch-release obligations)" | QP authority. |
| GDPR | Reg. (EU) 2016/679 | "GDPR Arts. 6, 9 (special-category health data), 22 (automated decision-making), 32 (security), 35 (DPIA)" | |
| ISPE | GAMP 5 | "ISPE GAMP 5 (2nd Edition, 2022)" | |
| PIC/S | PI 041 | "PIC/S PI 041 — Good Practices for Data Management and Integrity in Regulated GMP/GDP Environments" | |
| ISO | 14971:2019 | "ISO 14971:2019 — Medical Devices — Application of Risk Management" | |
| ISO | 13485:2016 | "ISO 13485:2016 — Medical Devices — Quality Management Systems" | |
| ISO | 27001:2022 | "ISO/IEC 27001:2022 — Information Security Management Systems" | |
| ISO | 42001:2023 | "ISO/IEC 42001:2023 — Artificial Intelligence Management System" | |

**Rule:** if you cite a regulatory document not on this table, add it here first with its verified current title + date. If you cite a document with a date that doesn't match this table, you have a citation defect to fix.

### 2A.2 21 CFR Part 11 sub-section authority map

| Sub-section | What it covers | Required in URS when... |
|---|---|---|
| § 11.10(a) | Procedures and controls protecting electronic-record validity | Always (procedural-control statement) |
| § 11.10(b) | Generating accurate and complete copies | When export / inspection-readiness is in scope |
| § 11.10(c) | Protection of records throughout retention period | Always (retention statement) |
| § 11.10(d) | Limiting access to authorized individuals | Always (access control) |
| § 11.10(e) | Operational audit trail | Always (audit trail) |
| § 11.10(g) | Use of authority checks | When role-based access matters |
| § 11.10(k) | System operation manuals + change control | When SDLC / change control is in scope |
| § 11.30 | Open systems — additional controls | When the system is internet-exposed |
| § 11.50 | Electronic-signature manifestations (name, date, meaning) | Every URS with e-signatures |
| § 11.70 | Signature/record linking | Every URS with e-signatures |
| § 11.100 | Uniqueness — no reuse / reassignment | Every URS with e-signatures |
| § 11.200 | Components of identity-based signatures (re-auth) | Every URS with e-signatures at critical moments |
| § 11.300 | Password and credential controls | Every URS with user authentication |

**Rule:** the URS must cite the **specific sub-section** being implemented per requirement — never a generic "21 CFR Part 11". A reviewer cannot test a generic citation.

### 2A.3 ICH M10 section numbering — the bioanalytical map

ICH M10 (Step 4, 24 May 2022) is structured around two method categories (chromatographic + ligand-binding) with parallel section trees. Common hallucinations: § 6.1.3 (does not exist), § 6.4 (does not exist), § 6.6 (does not exist).

| Topic | Chromatographic | Ligand-binding (LBA) |
|---|---|---|
| Method validation parameters | § 3 | § 4 |
| Selectivity, specificity, calibration curve, accuracy, precision, sensitivity, dilution integrity, matrix effect, recovery, carryover, stability | § 3.x sub-sections | § 4.x sub-sections |
| Run acceptance criteria | **§ 3.3.2** | **§ 4.3.2** |
| Reanalysis / repeat analysis | **§ 3.3.4** | **§ 4.3.4** |
| Incurred Sample Reanalysis (ISR) | **§ 5** (shared section) | **§ 5** (shared section) |
| Partial validation / cross-validation | **§ 6.1** | **§ 6.1** |

**Rule:** if your URS references ICH M10, cite the section number against the method category it applies to. Citing "§ 6.1.3" / "§ 6.4" / "§ 6.6" is a hallucination — these sections do not exist in M10.

### 2A.4 EU MDR PSUR cadence rule (Art. 86)

EU MDR Reg. 2017/745 Art. 86(1) cadence — verify before authoring any PMS / PSUR URS:

| Device class | Periodic report type | Cadence |
|---|---|---|
| Class I | **PMSR** per Art. 85 | Per Art. 85 (no PSUR cadence; report cadence per § 85(1)) |
| Class IIa | **PSUR** per Art. 86 | **At least every 2 years** |
| Class IIb | **PSUR** per Art. 86 | **At least annually** |
| Class III | **PSUR** per Art. 86 | **At least annually** + Notified-Body assessment |
| Implantable (any class) | **PSUR** per Art. 86 | **At least annually** + Notified-Body assessment |

**Rule:** never write "Class III + implantables annually; otherwise every 2 years" — that omits Class IIb. Class IIb is annual. Class IIa is biennial. Class I uses PMSR (different artefact).

### 2A.5 21 CFR Part 58 GLP role rules

| Role | Authority |
|---|---|
| Study Director | § 58.33 — sole point of overall study responsibility. |
| Principal Investigator | Not separately CFR-defined; multi-site GLP convention per OECD GLP Principle 1.3 / 2.2. When using the PI role in a URS, do NOT cite "§ 58.33(b)" as the binding (the sub-clause does not define a PI). |
| Quality Assurance Unit (QAU) | § 58.35 — independent QA function reporting outside the operations chain (§ 58.35(b)). |
| Archivist | § 58.190 — sole gateway to archived records; § 58.195 sets retention. |

**Rule:** when a URS introduces a Principal Investigator role, frame it as "multi-site GLP convention per OECD" — never bind to a fictional CFR sub-section.

### 2A.6 DACH authority assignment matrix

Which German / Austrian / Swiss authority covers what:

| Domain | DE | AT | CH |
|---|---|---|---|
| Medicinal products (drugs) | **BfArM** | AGES PharmMed | Swissmedic |
| Medical devices | **BfArM** | AGES MedMed | Swissmedic |
| Biological medicinal products / vaccines | **Paul-Ehrlich-Institut (PEI)** | AGES PharmMed | Swissmedic |
| Good Laboratory Practice (GLP) monitoring | **BfR GLP-Bundesstelle + Länder authorities** — NOT BfArM | AGES (per OECD) | Swissmedic GLP unit |
| Clinical trial submissions (CTIS) | BfArM (medicines) + PEI (biologicals) | AGES | Swissmedic |
| Vigilance / pharmacovigilance (medicines) | BfArM + PEI | AGES | Swissmedic |
| Vigilance / post-market surveillance (devices, EU MDR) | BfArM | AGES | Swissmedic (CH-specific regime per MepV) |

**Rule:** **BfArM is NOT the German GLP authority.** German GLP monitoring runs through BfR's GLP Federal Bureau (GLP-Bundesstelle) plus Länder (state) authorities. If a URS deals with GLP studies in Germany, cite BfR — not BfArM.

### 2A.7 URS-ID → FS-ID traceability rule

For every URS↔FS pair:

1. **The URS is FS-namespace-independent.** URS § 5 defines the canonical URS-IDs and their `shall`-clauses. The URS does NOT embed FS-IDs anywhere. There is no URS Appendix A — the URS as a document is owned by the business / process owner and must remain stable across FS-side namespace evolution.
2. **Every URS-ID in URS § 5 MUST appear individually in FS § 4 (Functional Specifications) as its own row.** No range compression (`URS-PART11-01..07`) — each ID gets its own row.
3. **Every URS-ID MUST also appear in FS § 8 (Appendix A — Traceability Matrix) as its own row.** Same no-range-compression rule.
4. **FS § 8 is the SOLE URS↔FS traceability surface in the corpus.** The RTM (Requirements Traceability Matrix) lives in the FS, not in the URS. Inspectors auditing traceability read FS § 8.
5. Each FS row in § 4 should give **per-ID specific implementation detail** — not generic text repeated across IDs.
6. An FS-ID that does not map to any URS-ID is an orphan and must be either removed or justified (e.g., FS-side-only implementation detail).
7. A URS-ID with no corresponding FS-ID is an unimplemented requirement and must be flagged in the FS revision history.

**Why this design:**

- **Coupling-direction discipline.** The FS depends on the URS; the URS does not depend on the FS. Embedding FS-IDs in the URS would force URS re-issue (with its higher governance bar) every time the FS namespace evolves — inverting the intended hierarchy where the business-stable artefact stays stable.
- **RTM lives where it can stay current.** FS § 8 is owned by the engineering / validation team and changes at FS-revision cadence. Duplicating the matrix back into the URS produces stale URS appendices and creates change-control friction with no regulatory benefit.
- **Range-compression breaks audit.** A reviewer cannot test "the range" — they can only test individual requirements against individual implementations.

**Earlier methodology iterations** required a URS Appendix A — Traceability Seed (URS-ID → planned FS-ID → planned Test-ID) inside every URS. That requirement was removed in v1.2 after external review (3-0 LLM council verdict + author decision) concluded the URS↔FS namespace coupling was operationally harmful and the duplication was not audit-required. See CHANGELOG v1.2 entry for the decoupling.

### 2A.8 `shall` / `must` discipline

Normative verbs in regulated specifications carry meaning:

| Verb | When to use |
|---|---|
| **shall** | System requirements. Default normative verb for URS / FS lines. "The system shall log..." |
| **should** | Recommendations, non-mandatory best practice. Rare in URS/FS; if used, must be clearly flagged as non-binding. |
| **must** | ONLY for constraints on parties OTHER than the system itself: downstream consumers ("consumers must not silently consume nulls"), operators ("the Quality Unit must review..."), or in quoted regulatory text ("FDA: 'you must review the AI-generated documents...'"). |
| **may** | Permissions / optional behaviour. "The system may auto-approve when..." |
| **will** | Forbidden in URS / FS — ambiguous between future tense and obligation; replace with `shall`. |

**Rule:** every system-requirement line uses `shall`. Every `must` occurrence in a URS must be either (a) constraining a non-system party or (b) in quoted regulatory text. The validation lint catches violations.

### 2A.9 YAML frontmatter rules

Frontmatter is parsed automatically by the disclosure-verification pass. To avoid parse failures:

1. **Required fields:** `artifact_class`, `artifact_status`, `generator`, `seed_corpus_basis` (list), `do_not_use_as` (list), `intended_use` (list), `labelling` (object with `evidence_level`, `signature_status`, `production_status`, `source_risk`).
2. **Strings containing `:` or `;` or em-dashes (—) MUST be quoted** with double-quotes. Example: `generator: "Claude (Anthropic) — inline batch, 2026-04-27"`. Unquoted strings with embedded `:` break the YAML parser because the parser tries to interpret the part before the colon as a key.
3. **Lists should use block style for any item with embedded punctuation:**
   - Bad (flow-style with colons): `seed_corpus_basis: [ISO 14971:2019, ISO 13485:2016]`
   - Good (block-style, quoted): `seed_corpus_basis:` then `- "ISO 14971:2019"` `- "ISO 13485:2016"`
4. **`do_not_use_as` MUST contain `regulated_record`** and SHOULD contain `basis_for_real_validation_decisions`.
5. **`labelling.source_risk` MUST equal `ai_authored_disclosed`** — this is the machine-verifiable disclosure flag.

### 2A.10 GAMP-category-coherence rule

If the URS declares a GAMP category, the structure MUST match:

| Category | Structural requirements |
|---|---|
| **Cat 1 (Infrastructure)** | No IQ/OQ/PQ for the infra itself; cite IT infrastructure qualification protocols; configuration management focus. |
| **Cat 3 (Non-Configurable COTS)** | IQ + OQ in acceptance; no PQ for the COTS itself; vendor-SDLC reliance section required. |
| **Cat 4 (Configured Products)** | IQ + OQ + PQ; configuration-specification section; vendor + site responsibility split. |
| **Cat 5 (Custom / Site-Developed)** | IQ + OQ + PQ; custom-development-lifecycle section; site-SDLC documentation; per-version validation evidence. |

If a URS declares Cat 4 but lacks `§ 5.x Software Configuration Requirements`, it is incoherent. If it declares Cat 5 but lacks `§ 5.x SDLC + per-version validation`, it is incoherent. The validation pass catches structural incoherence.

### 2A.11 EU AI Act high-risk-AI obligations checklist

For any URS describing a high-risk AI system per EU AI Act 2024/1689 (Art. 6 + Annex III), the URS must address (one or more requirements per article):

| Article | Topic |
|---|---|
| Art. 9 | Risk management system |
| Art. 10 | Data governance + training data quality |
| Art. 11 | Technical documentation (the "Art. 11 pack") |
| Art. 12 | Record-keeping / logging |
| Art. 13 | Transparency to deployers |
| Art. 14 | Human oversight (Human Oversight Operator role) |
| Art. 15 | Accuracy + robustness + cybersecurity |
| Art. 17 | Quality management system |
| Art. 43 | Conformity assessment (where applicable — Notified Body involvement) |
| Art. 50 | Transparency to natural persons (AI-generated content labelling) |
| Art. 72 | Post-market monitoring |
| Art. 73 | Serious-incident reporting to competent authority |

**Deadline reminder:** see § 2A.14 for the **Annex I (2 August 2027) vs Annex III (2 August 2026)** distinction — most pharma / medical-device AI is Annex I and inherits the **2027** deadline, not 2026.

### 2A.12 Document-structure invariants (all URS)

Every URS MUST contain, in this order:

1. YAML frontmatter (per § 2A.9)
2. H1 title `# User Requirements Specification (URS)`
3. H2 system title `## <System name> — <Vendor product or descriptor>`
4. Document Control table (placeholders for author / reviewer(s) / approver(s) with role labels). The Document Control block MUST include the **Project Mode** declaration line per § 2A.15.
5. Revision History table
6. Definitions table
7. § 1 Purpose
8. § 2 Scope (in / out)
9. § 3 System Description and Intended Use (with declared GAMP category)
10. § 4 User Roles (table with permissions + SoD enforcement)
11. § 5 User Requirements (sub-sectioned per § 2A.10 category rules; each requirement: ID + Priority H/M/L + Risk R1/R2/R3 + verifiable `shall`-clause)
12. § 6 Acceptance Criteria (lists FS, CS, RA, IQ, OQ, PQ, VSR, RTM deliverables)
13. § 7 Constraints
14. § 8 Assumptions
15. § 9 References (organised by jurisdiction — US / EU / DACH / International / Vendor)

The URS ends after § 9 References. **There is NO § 10 Top-level Risks in the URS** — implementation risks live in FS § 9 Implementation Risk Register per § 2A.16. **There is NO § 11 Appendix A in the URS** — URS↔FS traceability lives exclusively in FS § 8 (see § 2A.7). The URS is FS-namespace-independent and risk-register-independent.

**Filename version convention (v1.3, 2026-05-13):** every corpus file is named `<descriptive_slug>_URS_v<X.Y>.md` or `<descriptive_slug>_FS_v<X.Y>.md`. The `v<X.Y>` suffix MUST track the current content revision — bumped on every CHANGELOG entry that touches the file (not on each in-place edit during a single revision). At v1.3, all 100 files were renamed from `_v1.0.md` (their original-generation filename) to `_v1.3.md` to align filename with content; the rename was a one-time correction and locks the convention going forward. The Document Number inside the file (`<PREFIX>-URS-<TYPE>-NNN`) is the stable identifier across revisions; only the filename suffix changes when version bumps.

**Rationale for removing § 9 Top-level Risks from URS (v1.3, 2026-05-13):** A URS captures user needs / requirements (wishes). A wish does not have risks — only an implementation can fail. The risks previously catalogued in URS § 9 (mid-study amendment defects, integration drift, configuration errors, credential compromise, etc.) are **implementation, configuration, integration, and operational risks** — properties of the chosen system / its build / its runtime. These belong in the FS (which describes the implementation) or in the standalone Risk Assessment document (which performs the formal FMEA / HAZOP). The per-requirement Risk class column (R1/R2/R3) stays on every URS requirement — that is GxP-criticality of the requirement itself (what happens if the user need is not met), not implementation risk, and is correctly an attribute of the wish.

Every FS MUST contain, in this order:

1. YAML frontmatter with `parent_urs` pointer
2. H1 `# Functional Specification (FS)`
3. H2 with `Document Number`, `Version`, `Parent URS`, `Site`, `System Class`, `Regulatory Scope`
4. Document Control + Revision History (at the top, before numbered sections)
5. § 1 Purpose
6. § 2 Scope
7. § 3 System Architecture (text + ASCII diagram)
8. § 4 Functional Specifications (table with FS-ID + URS-ID + Specification — **one row per URS-ID**, no range compression)
9. § 5 Interface Specifications (where applicable) / Configuration Items (CI table)
10. § 6 Data Model / Configuration Risks (FS-level, narrowly scoped to configuration choices)
11. § 7 References (US / EU / DACH / International / Vendor)
12. § 8 Appendix A — URS → FS Traceability Matrix (**one row per URS-ID**)
13. **§ 9 Implementation Risk Register** (NEW in v1.3 — per § 2A.16. Last numbered section. Implementation / integration / configuration / operational / runtime risks. Replaces the URS § 9 Top-level Risks removed in v1.3.)

Section numbering above is the canonical pattern. Actual FS files may carry additional intermediate sections (e.g., separate § 5 Interface Specs and § 6 Data Model and § 7 Non-Functional Specs in T3/T4 systems) — in that case the Implementation Risk Register is always added as the **final numbered section** after the Traceability Matrix, with its own number reflecting actual local numbering.

### 2A.13 Tier-based requirement-count target (per URS / FS)

System complexity drives target requirement-count + URS line-count. Authoring an LIMS or EDC with only 30 requirements is incomplete — these systems carry real-world specifications of 100-200+ requirements. Conversely, padding a Karl Fischer instrument URS to 200 requirements is bloat.

| Tier | System character | URS requirement count | URS line target |
|---|---|---|---|
| **T1 — Small / simple instruments + utilities** | Cat 3 standalone instruments (Karl Fischer, particle counter, simple pH-meters); minor Cat 1 utilities | **30–50 requirements** | 300–400 L |
| **T2 — Standard lab instruments + mid-complexity systems** | Cat 4 configured lab instruments (HPLC, UV-Vis, NIR, dissolution, autoclave, tablet coater); standalone Cat 4 applications | **50–80 requirements** | 400–550 L |
| **T3 — Large enterprise systems** | LIMS, ELN, eQMS, EDMS, RIM, RTRT, production SCADA, large pharma application platforms | **100–150 requirements** | 600–900 L |
| **T4 — Mission-critical / highly-complex systems** | EDC, CTMS, eTMF, Veeva Vault Submissions, MES PAS-X, GenAI LLM Service, AI/ML Model Server, Pharmacovigilance DB | **150–250 requirements** | 900–1500 L |

**Rules:**

1. The tier is declared in the URS Revision History entry that drives the requirement count.
2. Tier lower bound is the floor — author up if the system genuinely warrants more depth.
3. Tier upper bound is the ceiling — exceeding it is acceptable when the system spans multiple sub-domains (e.g., MES PAS-X covers EBR + Recipe + Order + Material + Equipment in one platform).
4. The paired FS scales proportionally — each new URS-ID gets its own FS-ID row in § 4 and § 8 (per § 2A.7).
5. Tier choice is justified in 1-2 lines in the URS Revision History: "Authored to Tier T3 (LIMS-class enterprise system; 120-req target; spans sample lifecycle + method registry + run review + reporting + integration)."

### 2A.14 EU AI Act 2024/1689 — classification rule and per-Article URS coverage

The EU AI Act distinguishes **two high-risk classifications** with **different effective dates**. Getting this wrong is a credibility hit — most pharma AI is Annex I, not Annex III.

#### Classification decision tree

| Classification | Scope | Effective date |
|---|---|---|
| **Annex III high-risk** | AI deployed in 8 listed domains: (1) biometric identification, (2) critical infrastructure mgmt, (3) education + vocational training, (4) employment + worker mgmt, (5) access to essential services, (6) law enforcement, (7) migration / asylum / border control, (8) administration of justice / democratic processes | **2 August 2026** |
| **Annex I high-risk** | AI as a **safety component of a regulated product** (medical device, IVD, machinery, automobile, toy, etc.). Falls under the regulated product's existing CE-marking pathway. | **2 August 2027** (12-month extension over Annex III) |

**For pharma / GxP systems:**

- AI in a Software-as-a-Medical-Device (SaMD) context → **Annex I, 2027**
- AI in In Vitro Diagnostic (IVD) context (e.g., diagnostic decision support) → **Annex I, 2027**
- AI as safety component of a regulated medicinal product (e.g., dose-calculation AI in an automated drug-delivery device) → **Annex I, 2027**
- AI for **GxP decision-informing** in pharmaceutical manufacturing (e.g., RTRT decision rules, NIR PAT predictions feeding batch release) → **typically Annex I, 2027** because the AI is a safety component of the medicinal product's quality system
- AI for **general business workflow** in a pharma company (e.g., LLM gateway for drafting non-regulatory text) → **Article 50 transparency only** (not high-risk)
- AI for **access to essential medical services** (e.g., AI triage in healthcare insurance / hospital admission gating) → **Annex III, 2026**

**Rule:** if a URS describes AI that participates in a regulated-product / safety-component pathway, classify Annex I + deadline 2027. Cite both Annex I and the per-product regulation (MDR, IVDR, Machinery Directive) that brings it under the high-risk umbrella.

#### Provider obligations (Arts. 8–21) — required URS coverage

For Annex I/III high-risk systems, the URS MUST address each of these articles with ≥ 1 requirement set. (Annex I systems may inherit some via the underlying product regulation's QMS — note explicitly when this is the case.)

| Art. | Topic | Required URS coverage |
|---|---|---|
| 9 | Risk management system | Lifecycle risk-identification, mitigation, residual-risk acceptance — health, safety, fundamental rights |
| 10 | Data and data governance | Training / validation / test sets relevant, representative, statistically sound, documented provenance, bias mitigation. **This is the article the corpus directly serves.** |
| 11 + Annex IV | Technical documentation | Detailed dossier: architecture, training data, design choices, performance metrics, lifecycle changes. The "Art. 11 pack." |
| 12 | Record-keeping / logging | Automatic event logs, retained **≥ 6 months**, traceable |
| 13 | Transparency to deployers | Instructions for use specifying capabilities, limits, intended purpose, foreseeable misuse, accuracy/robustness/cybersecurity metrics, human-oversight measures, expected lifetime |
| 14 | Human oversight | Designed so a natural person can monitor, interpret outputs, override decisions, halt operation. **Two-person rule for real-time remote biometric ID.** |
| 15 | Accuracy, robustness, cybersecurity | Declared performance levels, resilience to errors / inconsistencies, protection against data poisoning, model evasion, confidentiality attacks |
| 17 | Quality management system | Documented QMS: design, V&V, data management, risk management, post-market monitoring, incident reporting. (Reads like GAMP 5 from a different angle.) |
| 18 | Documentation retention | **≥ 10 years after market placement** — must be in URS retention statements |
| 43, 47, 48 | Conformity assessment + CE marking + EU declaration of conformity | Before market placement. **Internal control (Annex VI)** or **notified-body assessment (Annex VII)** depending on category. Annex I systems typically inherit the product's existing notified-body pathway. |
| 49 | EU database registration | High-risk **Annex III** systems must be registered before placement (Annex I systems use the regulated product's existing registration). |
| 72 | Post-market monitoring | Active data collection from deployers |
| 73 | Serious incident reporting | To market surveillance authority within **15 days standard / 10 days if death / 2 days for widespread fundamental-rights infringement** |

#### Transparency obligation (Art. 50)

Applies to ALL AI systems (not just high-risk): AI-generated or AI-manipulated content must be labelled as such when shown to a natural person. URS must include a transparency-labelling requirement for any AI system that surfaces output to humans.

#### Deployer obligations (Art. 26)

When the corpus's user (deployer) is in a different role than the provider, URS should note deployer responsibilities:

- Use per provider's instructions; ensure input data relevant / representative
- Assign trained human oversight
- Monitor operation; suspend on risk; inform provider / authority
- Keep logs **≥ 6 months**
- Inform workers' representatives when used in workplace
- **FRIA (Fundamental Rights Impact Assessment)** before first deployment of certain Annex III systems (public bodies + private deployers in essential services). Not required for Annex I systems unless explicitly invoked.

#### Penalties (Art. 99) — for risk-table context

| Violation | Penalty cap |
|---|---|
| Prohibited AI practices (Art. 5 — social scoring, etc.) | up to **€35M or 7% global turnover** |
| High-risk non-compliance | up to **€15M or 3% global turnover** |
| Misleading information to authorities | up to **€7.5M or 1% global turnover** |

URS § 9 Risks table should reference Art. 99 penalty tier where AI non-compliance is a risk category.

#### Timeline (Art. 113)

| Date | Milestone | Corpus impact |
|---|---|---|
| 1 Aug 2024 | Entered into force | — |
| 2 Feb 2025 | Prohibited practices (Art. 5) + AI literacy obligations | URS should reference if system is in a workspace where AI literacy training applies |
| 2 Aug 2025 | GPAI obligations + governance bodies + penalties | GenAI LLM Service URS must reference GPAI obligations where the vendor LLM is GPAI-classified |
| **2 Aug 2026** | **Annex III high-risk + most of the rest** | Annex III systems — limited corpus application |
| **2 Aug 2027** | **Annex I high-risk (medical devices, machinery, etc.)** | **Default for pharma / SaMD / device AI in this corpus** |

#### Rule summary

1. Every URS that describes an AI system MUST declare its Annex I vs III classification (or "non-high-risk + Art. 50 transparency only") with 1-2 lines of rationale.
2. The compliance deadline cited MUST match the declared annex (2027 for I, 2026 for III).
3. The URS § 5 MUST contain ≥ 1 requirement set per applicable Art. 9–15 + 17 + 18 (with note where Annex I inherits via the underlying product regulation).
4. **EU AI Act non-conformance risk** lives in the paired FS § 9 Implementation Risk Register per § 2A.16 (was URS § 9 pre-v1.3), with Art. 99 penalty-tier awareness.
5. The URS § 9 References MUST cite the Articles bound, the underlying-product regulation (MDR / IVDR / Machinery) where Annex I, and the per-Art. timeline.

### 2A.15 Project Mode declaration rule (v1.3, 2026-05-13)

The GAMP 5 category alone is insufficient context for a business reader of the URS — "Category 4" tells a validation engineer the V-model depth, but does not tell a business stakeholder whether the platform was pre-selected (configuration project) or whether the URS is feeding vendor selection (RFP-feeder) or whether this is a custom build. Every URS Document Control block MUST therefore include a `Project Mode` line per the table below.

| GAMP cat | Project Mode wording |
|---|---|
| **Cat 4 — Configured Product (post-selection)** | `Project Mode: Configuration project on commercial software product <Vendor Product Name and Version> (GAMP 5 Category 4 — Configured Product; <hosting note>).` |
| **Cat 4 — Configured Product (pre-selection / RFP)** | `Project Mode: Platform selection project — requirements for RFP (vendor TBD) (GAMP 5 Category 4 — Configured Product).` |
| **Cat 5 — Custom / Site-Developed** | `Project Mode: Custom-build project — site-developed system (GAMP 5 Category 5 — Bespoke; internal SDLC).` |
| **Cat 3 — Non-Configurable COTS** | `Project Mode: Configuration project on non-configurable instrument / appliance <Product Name> (GAMP 5 Category 3 — Non-Configurable COTS).` |
| **Cat 1 — Infrastructure** | `Project Mode: Infrastructure qualification project (GAMP 5 Category 1 — Infrastructure).` |

Placement: the line sits in the Document Control block immediately under the `System Class (GAMP 5, 2nd ed.):` line, before the Document Control table. The line is mandatory in every URS authored to the v1.3 corpus standard.

**Origin:** convention exists in mature house templates (e.g., Roche / Genentech CSV SOP "Project Classification" block; PharmaLex "System Selection Status" field; Veeva Vault implementation-type tag) but is not literally called "Project Mode" in any of GAMP 5 v2 / PIC/S PI 011-3 / FDA CSA / EU Annex 11. This corpus standardises the label as `Project Mode` per the LLM Council verdict 2026-05-13.

### 2A.16 FS § 9 Implementation Risk Register rule (v1.3, 2026-05-13)

Implementation / configuration / integration / operational / runtime risks live in the paired FS, NOT in the URS. The FS § 9 Implementation Risk Register MUST contain (typical pattern):

```
## § 9. Implementation Risk Register

The risks below are properties of the implementation (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document). Per-requirement GxP-criticality (R1/R2/R3) stays on each URS requirement; it is not duplicated here.

| ID | Risk | Likelihood | Impact | Mitigation reference (URS-ID and/or FS-ID) | Implementation surface |
|---|---|---|---|---|---|
| FS-RISK-01 | <implementation risk> | L/M/H | L/M/H | URS-X-NN, FS-Y-MM | configuration / integration / runtime / operation |
| ...
```

The `Implementation surface` column distinguishes which layer of the implementation the risk lives on (configuration, integration boundary, runtime behaviour, operational use). T1 systems carry ≥4 entries; T4 systems carry ≥15. Full formal Risk Assessment (FMEA / HAZOP) remains a separate downstream artefact (`<DOC-PREFIX>-RA-<NN>`), not part of FS.

**Rationale:** see § 2A.12 "Rationale for removing § 9 Top-level Risks from URS." Per LLM Council verdict 2026-05-13 + user directive: a wish has no implementation risk; only an implementation does.

---

## 3. Contamination guarantee

The single most important property of this corpus for DACH pharma readers is that it is **not** derived from any client URS, internal Roche / Lonza / Merck KGaA / Bayer / Boehringer Ingelheim / Sanofi / any other party's validation documents. We document the engineering process that makes this verifiable.

### 3.1 The contamination guarantee (verifiable, not handwaved)

Every document in this corpus was generated from:

- The regulatory primary-source pack (see § 2.1)
- The system catalogue (curated archetypes, not derived from any client engagement)
- The structural-template prompt (the GAMP-aligned skeleton + invariants)
- The per-document originality seed (fictional company name, fictional site, fictional document number prefix)

The corpus was **not** generated from:

- Any URS or FS document authored by Nabil Attia or by anyone at na IT Consulting GmbH for any client engagement
- Any anonymised or pseudonymised URS from any past engagement at Roche, Lonza, Merck KGaA, Pfizer, Sandoz, Bayer, Boehringer Ingelheim, Sanofi, or any other party
- Any URS scraped from any organisation's intranet, document management system, or controlled document repository
- Any URS shared by a current or past employee under or in violation of an NDA
- Any URS reproduced from a paid-subscription regulatory database

### 3.2 How the guarantee is verifiable

Four mechanisms:

**(a) Read-only source pack.** The generator's regulatory source pack is the only document set the generator reads at run time. The pack is hash-pinned and version-controlled; the hashes match the published regulatory documents. Anyone re-running the pipeline against the same pack can verify the pack contains no customer URS.

**(b) Open-source pipeline.** The generator scripts, prompts, system catalogue, and invariants are all in the repository under Apache 2.0. There is no hidden generation pass. Anyone can read the prompt that was used and confirm it contains no embedded customer text.

**(c) Per-document YAML disclosure.** Every document declares its `seed_corpus_basis` in YAML frontmatter, listing the regulatory frameworks the generator drew on. The basis names public frameworks — never a client URS.

**(d) Fictional-identifier audit.** Site names (Acme Pharmaceuticals, Lyrae Bioworks, Vela Therapeutics, Quartz Genomics, etc.) are fictional and chosen from constellation / Greek-mythology / synthetic naming conventions to make accidental name-collision with a real company unlikely. Document number prefixes (ACME-URS-LCMS-001, LYR-RA-MLSRV-001) are fictional and follow visibly synthetic patterns. Personnel names are placeholder underscores in document control tables. Dates are marked `*(synthetic)*` inline.

### 3.3 What this means for a DACH Quality Unit

If your QA team reviews this corpus and asks "are you sure none of this came from a Roche URS?" — the answer is, in this order:

1. *No.* The generator never read a Roche URS. The pack the generator reads is the regulatory source pack, hash-pinned.
2. *Verifiable.* The pipeline is open-source. You can read the prompt and the system catalogue and confirm there is no customer text in either.
3. *Per-document.* Every document declares its seed-corpus basis in YAML. The basis names public frameworks.
4. *Fictional identifiers.* The site / company / personnel / document number identifiers are intentionally fictional and chosen from synthetic patterns to make false-positive collisions with real entities unlikely.

If the QA team still wants to do their own contamination review, they can: (a) read the generator prompt; (b) read the system catalogue; (c) hash the regulatory source pack against the published regulatory documents; (d) optionally re-run the pipeline against the same pack and verify the documents are of the same shape. That is the audit trail.

---

## 4. Day-30 evaluation rubric

When the Qwen 3 7B model is fine-tuned on this corpus (Day 30 of the campaign) and released, the question regulated readers will ask is: "Is the model's output actually usable?" The eval rubric below is the contract for what "usable" means.

A separate file `EVAL_RUBRIC.md` carries the full machine-readable rubric. This section summarises the philosophy and the dimensions.

### 4.1 Philosophy

A fine-tuned GxP URS-generating model is **useful** if its output is consistently a credible *starting point* for a real validation engineer — not a finished URS. The model produces a *draft*; the engineer's job is to (a) verify the regulatory anchoring, (b) inject the site-specific configuration, (c) submit it through the Quality Unit's change-control process. The model does not replace the engineer; the model lowers the engineer's setup cost.

The eval rubric is therefore not "is the URS correct" — it is "is this a credible first draft that a competent engineer can iterate on without rewriting from scratch."

### 4.2 Six evaluation dimensions

Each evaluated on a 0–5 scale by a human QA reviewer (1 reviewer minimum, 2 for inter-rater reliability on a sub-sample). A document is "usable" if it scores ≥ 3 on every dimension and ≥ 4 on dimensions 1, 2, and 5.

| # | Dimension | What's being scored | 0 (fail) | 3 (acceptable) | 5 (excellent) |
|---|---|---|---|---|---|
| 1 | **Structural completeness** | Are all GAMP 5 canonical sections present and in the right order? | Multiple sections missing or out of order | All sections present and in order | All sections present, in order, with sub-section breakouts where appropriate |
| 2 | **Regulatory accuracy** | Do all regulatory citations resolve to real, currently-effective documents? Are sub-section references correct? | Hallucinated guidances or wrong section numbers | All citations resolve and are correctly versioned | All citations resolve, are correctly versioned, and bind to the system's category accurately |
| 3 | **GAMP categorisation coherence** | Does the document's GAMP category drive its validation depth? | Category claimed but structure contradicts | Category claimed and structure matches | Category claimed, structure matches, and category-specific concerns (e.g., custom-development controls for Cat 5) are addressed |
| 4 | **Requirement testability** | Is every requirement a verifiable `shall`-clause with a clear test target? | Vague adjective-stacked requirements ("the system shall be robust") | Most requirements verifiable; isolated weak phrasing | All requirements verifiable; testability evident at line level |
| 5 | **Traceability** | Does every URS-ID appear in Appendix A with a planned FS-ID and IQ/OQ/PQ test? | No traceability seed or major coverage gaps | Most URS-IDs traced; minor gaps | All URS-IDs traced; FS pairs cross-reference correctly |
| 6 | **`shall`/`must` discipline** | Is `shall` used for system requirements; `must` reserved for constraints on consumers/processes? | Mixed or inverted usage | Mostly correct; isolated `must` creep | Discipline maintained throughout |

### 4.3 Pass / fail definition

- **Pass:** ≥ 4 on dimensions 1, 2, 5; ≥ 3 on dimensions 3, 4, 6. (i.e., the structure is right, the citations resolve, the traceability is there; the rest is acceptable for a first-draft.)
- **Fail:** Any dimension scores 0; or two or more dimensions score below the threshold.

### 4.4 Eval sample size

For the Day-30 release, the eval is run on a stratified random sample of 30 generated documents:

- 6 Cat 4 lab instruments
- 6 Cat 4 production control systems
- 6 Cat 4 enterprise quality applications
- 6 Cat 5 custom-developed (AI/ML included)
- 3 Cat 1 infrastructure
- 3 GAMP-category-mixed edge cases

Sample size is fixed at 30 to give 95% confidence intervals on a binary pass/fail rate of ±15 percentage points. Larger eval sets are welcomed in v1.1 work.

### 4.5 Reviewer profile

The Day-30 eval is performed by:

- 1 senior validation engineer with ≥ 10 years of GxP CSV experience and direct exposure to FDA / EMA inspection
- 1 QA reviewer at Quality Unit level with authorisation to approve URS in production at a regulated site

Both reviewers are blind to which documents are model-generated versus which are corpus-template-derived (this matters for inter-rater reliability — the question is whether the model produces *credibly usable* drafts, not whether the model produces *distinguishable-from-corpus* drafts).

Reviewers' identifications are blinded in the published eval report.

### 4.6 What the eval cannot prove

The eval cannot prove a model-generated draft would survive a real regulatory inspection. The only thing that proves that is: a Quality Unit reviewing the draft, editing it, signing it, and the inspector accepting it. The eval scores whether the draft is a credible *starting point* — that is the contract.

---

## 5. License posture

Two separate licenses, both permissive:

| Asset | License | Why |
|---|---|---|
| **Dataset** (the 50 URS + 50 FS) | **CC-BY-SA 4.0** | Conventional for synthetic datasets; preserves attribution; share-alike encourages downstream community contribution |
| **Pipeline / scripts / prompts / methodology** | **Apache 2.0** | Permissive; consistent with Qwen 3's license; enables derivative deployment in commercial regulated environments |
| **Methodology document** (this file) | **Apache 2.0** | Same as pipeline — the methodology is engineering work, not data |

The two licenses are deliberately separate. The dataset's CC-BY-SA-4.0 share-alike protects the dataset's downstream evolution. The pipeline's Apache 2.0 enables a DACH pharma's internal IT team to fork the pipeline, point it at their own internal regulatory pack, and generate their own house-style URS templates *without* CC-BY-SA's share-alike obligation propagating into their internal IP.

---

## 6. Contact and feedback

Open an issue on the GitHub repository, or email nat@naitc.de.

We welcome:

- Corrections to regulatory citations (with reference to the primary source)
- Examples of where the corpus reads off-house-style relative to your industry context (named-house-style submissions accepted under CC-BY-SA 4.0 attribution)
- Patches to the generator prompts that improve the GAMP-category-coherence check or add a new framework binding
- Re-generation pull requests against the published source pack

We do not accept:

- Anonymised client URS as contributions (the contamination guarantee in § 3 is non-negotiable)
- Pull requests that introduce hallucinated regulatory citations
- Pull requests that remove the YAML disclosure block from any document

---

## 7. Review history

### 7.1 Internal pre-release review (v1.1, 2026-05-11)

Initial v1.1 release after hand-expansion of 7 priority URS + 7 paired FS docs. Internal review passed all six post-generation checks of § 1.2 Stage 6.

### 7.2 External quality review (2026-05-12, pre-kickoff)

An independent quality review pass on v1.1 surfaced regulatory-citation defects that would have failed DACH pharma QA scrutiny. **The review was the proximate cause of the v1.1.1 corrections** documented in `CHANGELOG.md`. Categories of defect found, all now fixed:

- **Citation currency drift** — FDA CSA cited as Sep 2025 (superseded by Feb 2026); FDA PCCP cited as 2024 AI/ML (superseded by Aug 2025 AI-Enabled).
- **Hallucinated regulator sub-sections** — ICH M10 § 6.1.3 / § 6.4 / § 6.6 (none of which exist).
- **Wrong regulator-document designation** — ICH E6(R3) cited as "2026 revised" instead of "Step 4, adopted 6 January 2025".
- **Regulatory-content errors** — EU MDR PSUR cadence omitted Class IIb (must be annual, not biennial); 21 CFR § 58.33(b) misused to bind a Principal Investigator role (PI not CFR-defined); BfArM misidentified as German GLP authority (BfR GLP-Bundesstelle is correct).
- **Structural defects** — 5 of 7 paired FS used range-compression (`URS-PART11-01..07 → FS-PART11-01..07`) violating the per-ID traceability rule.
- **YAML frontmatter parse errors** in 2 files (em-dash + colon issues).
- **Discipline drift** — 1 `must` used where `shall` was required.

**Reviewer:** independent quality-review pass by Codex (OpenAI), prompted to check hallucinated citations, traceability gaps, `shall`/`must` discipline, YAML parseability, and methodology-vs-reality consistency. Review duration: 16 min 44 s.

**Recommendation accepted in full.** All findings rated CRITICAL or HIGH were patched before the v1.1.1 release. The rules in § 2A.1–2A.12 were derived from this review — they encode the failure modes found so future generation runs catch them at validation time rather than after publication.

### 7.3 Validation pass at v1.1.1 release

All six post-generation checks (§ 1.2 Stage 6) re-run after the corrections:

- ✅ `shall`/`must` lint — clean (10 `must` occurrences, all on downstream consumers / quoted regulator text)
- ✅ Citation accuracy — all citations verified against current effective versions per § 2A.1 table
- ✅ GAMP-category coherence — all 7 v1.1 URS structurally match their declared category
- ✅ Traceability seed coverage — 100% URS-ID coverage in FS § 4 and § 8 across all 7 pairs
- ✅ YAML frontmatter — 100/100 corpus files parse cleanly with valid disclosures
- ✅ Length sanity — all 50 URS ≥ 150 lines; median 196 lines

---

**Methodology version:** 1.1.1 · **Released:** 2026-05-13 · **License:** Apache 2.0
