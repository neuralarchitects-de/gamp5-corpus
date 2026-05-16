# Changelog — GAMP 5 Synthetic Design Specification Corpus

All notable changes to the DS corpus are documented here. The corpus follows semantic-ish versioning: MAJOR.MINOR — the MINOR digit bumps on every release that touches any DS file (per METHODOLOGY § 2B.9 filename version convention).

---

## v1.1 — 2026-05-16 — Codex review patch

Independent quality-review pass by Codex (OpenAI) on the v1.0 release surfaced 3 HIGH + 3 MED + 2 LOW findings. All HIGH + MED items patched before v1.1 promotion.

### HIGH-1 — Broken parent paths
Frontmatter `parent_fs.file` + `parent_urs.file` paths used `../../...` but DS files live at `DS/_generated/final/` — the correct relative path is `../../../...` (three levels up to `sample-gamp-docs/`, then down into the sibling folder). Fixed in all 36 affected files. METHODOLOGY § 2.2 path example also corrected.

### HIGH-2 — Cat 3 / Cat 4 contradiction
- `Indus_Therapeutics_Karl_Fischer_DS_v1.1.md` (was v1.0): System Class line declared "Category 4 — Configured Product (DS adopts Cat 3 — Vendor-Design-Reliance Statement posture)" — internally contradictory. Reframed to "Category 3 — Non-Configurable COTS" with matching Project Mode wording per § 2A.10 + § 2A.15.
- `Drumlin_Diagnostics_Particle_Counter_DS_v1.1.md` (was v1.0): same pattern. Same fix.

### HIGH-3 — EU AI Act Annex I penalty tier overstated
`Hesperia_BioPharma_RTRT_DS_v1.1.md` (was v1.0) cited the Art. 99 penalty cap as "€35M / 7% global turnover" on 4 lines (Regulatory Scope reference; DR-17 risk-register entry; § 8 narrative; § 8 Article coverage table) — that tier applies only to prohibited Art. 5 practices per Art. 99(3). Annex I high-risk non-compliance is "€15M / 3% global turnover" per Art. 99(4). All 4 occurrences corrected with explicit note clarifying when the higher tier would apply.

### MED-1 — URS-IDs in DS body
10 DS files cited URS-IDs (`URS-X-NN`) in body Justification columns, violating the DS↔FS-only traceability rule in § 2B.2 (DS coupling to URS is transitive via frontmatter `parent_urs` block; only FS-IDs should appear in body). 109 body references stripped corpus-wide. Files affected (URS-ID body counts at v1.0 → 0 at v1.1):

| File | v1.0 URS-IDs in body | v1.1 |
|---|---:|---:|
| Pyxis EMS | 20 | 0 |
| Vela Autoclave | 19 | 0 |
| Kymeta PI Historian | 16 | 0 |
| Selene Cold Chain | 12 | 0 |
| Phlox CMMS | 10 | 0 |
| Veridian MES PAS-X | 7 | 0 |
| Cetus Watson LIMS | 6 | 0 |
| Marigold EDC Rave | 6 | 0 |
| Vesper Cleaning Val | 6 | 0 |
| Hesperia RTRT | 4 | 0 |
| Cassia SCADA Water | 3 | 0 |
| **Total** | **109** | **0** |

Substring URS-IDs were replaced with the placeholder "(transitive via parent URS)". A separate restoration pass repaired 31 URS-document-number substrings (`<PREFIX>-URS-<DOMAIN>-NNN`) that were inadvertently mangled by the strip pattern (the URS doc-numbers contain the `URS-` substring; the regex was tightened to skip them — see the restore step in the patch script).

### MED-2 — Art. 50 transparency omission
`Tessera_Bio_CV_Inspection_DS_v1.1.md` (was v1.0) listed EU AI Act Arts. 8–21, 26, 43, 47–49, 72, 73, 99, 113 in its Regulatory Scope (line 39) + References (line 638) but omitted Art. 50 (transparency to natural persons — AI-generated content labelling). Art. 50 added on both lines, framed as "Art. 50 (transparency — synthetic-output labelling)" / "Art. 50 (transparency to natural persons — AI-generated content labelling)". This brings Tessera in line with Hydra, Lyrae, and Hesperia which already covered Art. 50.

### MED-3 — CIS Kubernetes Benchmark version-specific citations
4 Cat 5 SDS files (Hydra GenAI, Helios audit-trail, Lyrae AI/ML, Tessera CV) cited "CIS K8s Benchmark v1.9" — version-specific lock-in not externally verifiable at corpus release and likely stale (current CIS K8s Benchmark at corpus release is ≥ v1.12). 8 occurrences rewritten as "CIS Kubernetes Benchmark (current release at site deployment)" to defer the version pin to the deploying site. This matches the methodology's stance that infrastructure baselines are site-tracked and verified at deployment time.

### LOW-1 — README Cat-listing inconsistency
`README.md` Coverage section listed Lacuna Compendial Calculator Excel under "Category 3" alongside Karl Fischer + Particle Counter, but Lacuna is authored as a Cat 5 SDS hybrid (Excel 365 + user-developed formula library + named ranges + decision-boundary formulae per GAMP 5 2nd ed. § 8 escalation rule). The Cat 5 list cited 4 systems but the corpus has 5 (or 6 if RTRT is counted). README updated:
- Cat 3 list: now Indus Karl Fischer + Drumlin Particle Counter (2 systems).
- Cat 5 list: now Lyrae + Hydra + Helios + Tessera + Lacuna (5 systems). RTRT noted as Cat 5 SDS with Lyrae AI inference binding.

### LOW-2 — `will` / `should` descriptive usage
Corpus-wide scan found 4 `will` + 3 `should` matches. Manual review confirmed all were descriptive / future-tense / non-normative phrasing — not normative-verb violations. No release-blocking fix; no change made. Optional stylistic cleanup deferred to a future minor sweep.

### Mechanical changes (filename + version field)
- All 50 DS corpus files renamed `*_DS_v1.0.md` → `*_DS_v1.1.md` per § 2B.9 filename version convention.
- `**Version:**` field in each file's Design Control block bumped from `1.0` to `1.1` (7 markdown-bold form; 7 table-cell form; 5 YAML-frontmatter `version:` form — all variants handled).
- A v1.1 row appended to every DS Revision History table summarising the v1.1 patches.
- METHODOLOGY.md bumped 1.0 → 1.1; v1.1 changelog appended (§ 8 new); path example corrected.
- README.md updated for Cat 3 / Cat 5 listings + Cat 5 count fix.
- EVAL_RUBRIC.md bumped 1.0 → 1.1 (version-only bump; rubric content unchanged).

### Verification gates re-run at v1.1
- ✅ YAML + disclosures — 50/50 files
- ✅ Stale-citation grep — 0 hits (per § 2A.1–2A.6)
- ✅ Matrix-row range-compression — 0 (Aurora + Hydra + Quartz patched at v1.0; preserved at v1.1)
- ✅ Path resolution — 100% (all 100 `parent_fs.file` + `parent_urs.file` pointers resolve from each DS file's location)
- ✅ END marker — 50/50 files
- ✅ Document-number convention — 50/50 match pattern
- ✅ URS-IDs in DS body — 0 (down from 109 at v1.0)
- ✅ Cat 5 SDS files declare EU AI Act Annex classification correctly (Lyrae + Tessera + Hesperia = Annex I 2027; Hydra = per-use-case decision tree; Helios = explicit non-applicability)
- ✅ Tessera Art. 50 transparency coverage added
- ✅ CIS K8s Benchmark version-agnostic across 4 Cat 5 SDS files

### Reviewer
Independent quality-review pass by Codex (OpenAI), 25 min wall-clock, 3.77M tokens (3.45M cached). Recommendation: patch to v1.0.1 before release — adopted, but published as v1.1 per § 2B.9 filename version convention (the minor version digit tracks every release that touches DS files). Review report archived at `/tmp/codex-ds-review-2026-05-16.md`.

---

## v1.0 — 2026-05-15 — Initial DS corpus release

50 DS files generated via 7 parallel Claude agents, one DS per existing URS+FS pair. Framework files (METHODOLOGY.md, README.md, EVAL_RUBRIC.md) authored before generation.

### Coverage by GAMP category
- **Cat 1 (Infrastructure)** — 2 IDS files: Quartz Genomics AD, Aurora Backup
- **Cat 3 (Non-Configurable COTS)** — 2 thin Vendor-Reliance Statements: Indus Karl Fischer, Drumlin Particle Counter (note: declared Cat 4 in v1.0 by mistake; corrected at v1.1 per HIGH-2)
- **Cat 4 (Configured Products)** — 41 Configuration Specifications (CS), including 5 with embedded mini-SDS for site-developed code (Cassia SCADA Water, Pyxis EMS, Selene Cold Chain, Vesper Cleaning Val, Carina SPC, Halcyon Stability — Python / JSL / VB-Script extensions per § 2B.4 rule 6)
- **Cat 5 (Custom)** — 5 full Software Design Specifications (SDS): Lyrae AI/ML Model Server, Hydra GenAI LLM Service, Tessera CV Inspection, Helios Custom Audit-Trail Workbench, Hesperia RTRT (with Lyrae AI inference binding). Lacuna Compendial Calculator Excel authored as Cat 5 hybrid (Excel 365 + user-developed formula library).

### Tier distribution
- T1 (200–350 L): 2 files
- T2 (400–600 L): 20 files
- T3 (700–1100 L): 23 files
- T4 (≥ 1000 L): 3 files (Veridian MES PAS-X 1105 L, Marigold EDC Rave 1106 L, Hesperia RTRT 1003 L)

### Total corpus size
50 DS files + 3 framework files = ~33,694 lines.

### Post-generation patches at v1.0
- Aurora Backup + Hydra GenAI + Quartz AD: traceability matrix range-compression (`DS-XXX-NN..NN` rows) expanded to per-DS-ID rows per § 2B.2 rule 2. Aurora: 18 compressed rows → 87 per-ID rows + 5 risk-register cells fixed. Hydra: 4 compressed rows → 30 per-ID rows. Quartz: 14 compressed rows → 90 per-ID rows + 4 risk-register cells fixed.

---

**Changelog convention:** each release lists HIGH / MED / LOW findings as separate sub-sections. Mechanical changes (file renames, version-field bumps) are documented separately from substantive content fixes.

**License:** Apache 2.0 (the changelog is engineering work, not data).
