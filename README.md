# GAMP 5 Synthetic URS+FS Corpus

> 50 User Requirements Specifications (URS) + 50 paired Functional Specifications (FS)
> for GxP-regulated computer systems — open, free, and built from public regulatory sources.

[![License: CC BY-SA 4.0](https://img.shields.io/badge/license-CC%20BY--SA%204.0-blue.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
[![Release](https://img.shields.io/github/v/release/neuralarchitects-de/gamp5-corpus)](https://github.com/neuralarchitects-de/gamp5-corpus/releases)
![Files](https://img.shields.io/badge/files-100-blue)
![Lines](https://img.shields.io/badge/lines-42%2C997-blue)
![GAMP](https://img.shields.io/badge/GAMP-1%20%C2%B7%203%20%C2%B7%204%20%C2%B7%205-blue)

A public, openly-licensed reference corpus covering the regulated pharma / biotech / medical-device
system landscape — from compendial instruments to AI/ML platforms, enterprise quality systems,
clinical-trial systems, post-market and safety systems, and shared IT infrastructure. Generated
from primary regulatory sources (FDA, EMA, ICH, EU GMP Annex 11, EU AI Act, DACH authorities) and
paired with matching functional specifications.

**Hub page:** https://neuralarchitects.ae/gxp-corpus

---

## ⚠ Not a regulated record

Every file in this corpus carries `do_not_use_as: regulated_record` and
`labelling.source_risk: ai_authored_disclosed` in its YAML frontmatter. Companies, dates, and
identifiers are marked *(synthetic)*. **No FDA, EMA, BfArM, Swissmedic, or other competent
authority has reviewed or signed off on this material.**

If you derive an operational artefact from these templates, your Quality Unit **must** review,
edit, sign, and approve it under your own change-control before it has any regulated status.
Use this corpus as a starting point for house templates, RAG grounding, fine-tuning, or training
contrast sets — never as a drop-in deliverable.

---

## What's inside

```
gamp5-corpus/
├── README.md              (this file)
├── LICENSE                Creative Commons Attribution-ShareAlike 4.0
├── CITATION.cff           Citation metadata
├── CHANGELOG.md           v1.0 → v1.1 → v1.1.1 → v1.2 → v1.3
├── KNOWN_LIMITATIONS.md   Honest list of what the corpus does well / less well
├── METHODOLOGY.md         Canonical rule-set (§ 2A, the law)
├── EVAL_RUBRIC.md         Grading rubric for derived URS
├── URS/                   50× *_URS_v1.3.md
└── FS/                    50× *_FS_v1.3.md
```

### Tier system (METHODOLOGY § 2A.13)

Depth is sized to real-world system complexity.

| Tier | Class                                                | Target reqs | Examples |
|------|------------------------------------------------------|-------------|----------|
| T1   | Small / standalone instruments + utilities           | 30–50       | Karl Fischer, particle counter, compendial calculator |
| T2   | Configured lab instruments + mid-complexity apps     | 50–80       | UV-Vis, NIR, TOC, dissolution, SPC, stability, APR, LMS, autoclave, cold chain, EMS, BMS |
| T3   | Large enterprise + production systems                | 100–150     | LIMS, ELN, EDMS, eQMS, RIM, RTRT, SCADA, AD, audit-trail workbench, CV inspection |
| T4   | Mission-critical / multi-module                      | 150–250     | EDC, CTMS, eTMF, Vault Submissions, AI/ML Model Server, GenAI LLM Service, MES PAS-X, PV DB |

### Coverage at a glance

- **Lab instrumentation & analytics** — Chromatography, LC-MS, UV-Vis, NIR, TOC, dissolution, stability, SPC, APR, particle counter, Karl Fischer
- **Production & process control** — MES PAS-X, SCADA water systems, bioreactor / continuous fermentation, tablet coater, autoclave, lyophilizer, cold chain
- **Enterprise quality** — LIMS, ELN, EDMS, eQMS, ValGenesis VLM, Watson LIMS, RIM, RTRT, Annual Product Review
- **Clinical trials** — EDC, CTMS, eTMF, Vault Submissions, ePRO portal, LMS, randomisation, study build
- **Post-market & safety** — Pharmacovigilance DB (Argus), EU MDR PMS, Adverse Event DB, Submissions drafting
- **AI / ML / Custom Cat-5** — AI/ML Model Server, GenAI LLM Service, CV Inspection (sterile products), audit-trail workbench
- **Shared IT infrastructure** — Active Directory identity service, Backup tier (T1/T2/T3, RPO/RTO targets)

### Document anatomy

**URS** — single canonical structure (METHODOLOGY § 2A.12):
- § 1 Purpose · § 2 Scope · § 3 System description + GAMP category · § 4 User roles · § 5 Requirements (per-domain subsections, including 21 CFR Part 11, ALCOA+, EU AI Act where relevant) · § 6 Acceptance criteria · § 7 Constraints · § 8 Assumptions · § 9 References · END marker.
- Each requirement carries **ID + Priority (H/M/L) + Risk class (R1/R2/R3) + verifiable `shall`-clause**.
- From v1.3 every URS declares its **Project Mode** in the Document Control block (config-on-COTS, custom-build, infrastructure-qualification, or instrument-configuration).
- The URS is **FS-namespace-independent** — no Appendix A, no embedded FS-IDs.

**FS** — paired one-to-one with the URS:
- § 1 Purpose + seed_corpus_basis · § 2 Architecture · § 3 Component decomposition · § 4 Functional specifications (per-FS-ID rows citing originating URS-IDs) · § 5 Interface specs · § 6 Data + persistence · § 7 Non-functional behaviour · § 8 URS → FS Traceability Matrix (every URS-ID gets its own row, no range compression) · § 9 Implementation Risk Register (new in v1.3) · Revision history.

---

## How to use

### Read directly on GitHub
Every file is browsable in the repo tree.

### Clone the whole corpus
```sh
git clone https://github.com/neuralarchitects-de/gamp5-corpus.git
```

### Download as a single zip
- **Latest release**: https://github.com/neuralarchitects-de/gamp5-corpus/releases/latest
- **Mirror on the hub page**: https://neuralarchitects.ae/corpus/gxp-corpus-v1.3.zip

### Fine-tune or RAG-ground
The corpus is structured for supervised fine-tuning of regulated-industry specification authoring.
Pair each URS with its FS using filename matching (system name prefix), or use the explicit
traceability matrix in FS § 8. The METHODOLOGY file ships the authoring rules.

---

## How to cite

Short form:

> Attia, N. *GAMP 5 Synthetic URS+FS Corpus*, v1.3 (2026). NA IT Consulting
> (Neural Architects), Sandhausen, Germany. Licensed CC-BY-SA 4.0.

Full BibTeX / RIS / EndNote metadata in [`CITATION.cff`](./CITATION.cff). Right-click → "Cite this
repository" on GitHub also surfaces a one-click citation.

---

## License

Licensed under [**Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)**](https://creativecommons.org/licenses/by-sa/4.0/).

You can use, modify, and redistribute the templates — including for commercial purposes —
provided you **attribute** the corpus (see [`CITATION.cff`](./CITATION.cff)) and **license your
derived work under the same terms**. ShareAlike is intentional: it keeps the regulatory
ground-truth open as it spreads.

Full license text in [`LICENSE`](./LICENSE).

---

## Methodology

The canonical rule-set is [`METHODOLOGY.md`](./METHODOLOGY.md). Highlights from § 2A:

- **§ 2A.1** Citation currency table — FDA / EU / ICH / DACH / vendor primary sources, single source of truth.
- **§ 2A.2–2A.5** Sub-section maps for 21 CFR Part 11, ICH M10, EU MDR PSUR cadence, 21 CFR Part 58 GLP roles — locks out common citation defects.
- **§ 2A.6** DACH authority map (BfArM ≠ GLP authority; BfR + Länder = DE GLP).
- **§ 2A.7** URS↔FS traceability lives in FS § 4 + § 8 only.
- **§ 2A.8** `shall` for system requirements; `must` only for downstream-consumer constraints or quoted regulator text.
- **§ 2A.9** YAML frontmatter rules + disclosure invariants.
- **§ 2A.11** EU AI Act provider obligations Arts. 8–21.
- **§ 2A.12** URS / FS structure invariants (§ 1 → § 9 References → END; FS ends with Implementation Risk Register).
- **§ 2A.13** Tier system (T1–T4).
- **§ 2A.14** EU AI Act Annex I (SaMD / safety-component, 2 Aug 2027) vs Annex III (eight listed domains, 2 Aug 2026).
- **§ 2A.15** Project Mode declaration rule — new in v1.3.
- **§ 2A.16** FS § 9 Implementation Risk Register rule — new in v1.3.

Six structural + citation verification gates run after every wave; v1.3 (2026-05-13) passes all
six. See [`CHANGELOG.md`](./CHANGELOG.md) for full version history.

---

## Provenance

- **Author:** Nabil Attia (NA IT Consulting / Neural Architects), Sandhausen, Germany.
- **Authoring approach:** AI-augmented with multi-wave human-directed enrichment and external
  citation review. Each authoring agent works under METHODOLOGY § 2A and produces self-verified
  output. All AI authorship is disclosed in the YAML frontmatter.
- **No client data, no NDA material, no regulated records** were used. Sources are public regulator
  documents, ISPE GAMP 5 (2nd ed., 2022), ICH guidance, EU AI Act 2024/1689, and vendor public
  documentation.
- **Defects we have caught** (and how we keep them out): see [`KNOWN_LIMITATIONS.md`](./KNOWN_LIMITATIONS.md)
  and the CHANGELOG patch history under v1.1.1 and v1.3.

---

## Contributing

The corpus is structurally stable but not finished — citation accuracy, coverage breadth, and
authoring-style diversity all benefit from outside eyes.

- **Found a citation defect?** Open an issue with the file path, the quoted line, and the
  authoritative source. Cite-error reports are the highest-value contribution.
- **Coverage gap?** Open a discussion. We track planned additions in the CHANGELOG TODO list.
- **Structural issue** (broken traceability, missing END marker, YAML defect, etc.)? Open an issue
  with the offending file.
- **Want to submit a new URS+FS pair?** Open a draft PR. New pairs must follow METHODOLOGY § 2A
  end-to-end and pass the six verification gates before merge. The METHODOLOGY file is the
  contract.

Please read [`KNOWN_LIMITATIONS.md`](./KNOWN_LIMITATIONS.md) before opening an issue — many obvious
gaps are already tracked.

---

## Related

- **Website** — https://neuralarchitects.ae/gxp-corpus (download mirror + 1-page overview)
- **Hugging Face dataset** — *coming soon*
- **Contact** — contact@neuralarchitects.de
- **Author profile** — https://www.linkedin.com/in/nabil-attia/

---

*Generated and maintained by [Neural Architects](https://neuralarchitects.ae) — NA IT Consulting,
Sandhausen, Germany.*
