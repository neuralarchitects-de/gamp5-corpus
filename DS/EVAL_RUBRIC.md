# Evaluation Rubric — Human-QA Review of Generated Design Specifications

**Audience:** human reviewers (senior solution architect / validation engineer + QA reviewer) scoring documents produced by an LLM fine-tuned on the GAMP 5 synthetic URS+FS+DS corpus. The reviewer is asked to score whether the model's DS output is a **credible first-draft technical design** that a competent solution architect can iterate on without rewriting from scratch — not whether the DS is a regulatorily-signable design baseline.

**License:** Apache 2.0 (the rubric is engineering work, not data).

---

## What's being evaluated

The model output is a Design Specification (DS), Configuration Specification (CS), Software Design Specification (SDS), or Infrastructure Design Specification (IDS) — the specific variant determined by the GAMP category of the parent URS+FS pair. The model is given:

1. The parent URS file (read-only context)
2. The parent FS file (the authoritative input — DS-IDs map to FS-IDs)
3. A brief intended-use prompt (e.g., "Generate a Configuration Specification for the Cat 4 dissolution apparatus computer system described in `Solenne_Pharma_Dissolution_URS_v1.3.md` + `Solenne_Pharma_Dissolution_FS_v1.3.md`")

The rubric scores whether the model's output is a **credible first draft** that a competent solution architect can iterate on — see `METHODOLOGY.md` § 6 for the philosophy.

---

## Scoring instructions

For each document, score each of 6 dimensions on a 0–5 scale. Mark the time taken (in minutes) to review. Blind-flag any document that appears to plagiarise from a real client DS (this is a contamination check, not a pass/fail dimension).

Inter-rater reliability: 2 reviewers score the same sub-sample of 6 documents independently. Calculate Cohen's κ for each dimension. κ ≥ 0.60 (substantial agreement) is the threshold for the rubric being usable; below that, the rubric needs sharpening.

---

## Dimension 1 — Structural completeness (per-Cat-variant)

**What's scored:** Does the DS carry the GAMP-category-driven canonical sections in the right order? Does the variant declared (IDS / Cat-3 Reliance Statement / CS / SDS) match the parent system's GAMP category?

| Score | Definition |
|---|---|
| 5 | Variant correctly declared (matches parent Cat); all variant-specific mandatory sections present (per METHODOLOGY § 2B.1) + common preamble + tail; sub-section breakouts where appropriate (e.g., Cat 5 SDS § 5 Module Decomposition broken into ≥ 3 logical modules) |
| 4 | Variant correctly declared; all mandatory sections present; minor section ordering issue |
| 3 | Variant correctly declared; 1 mandatory section missing or merged |
| 2 | Variant correctly declared; 2 mandatory sections missing OR variant misdeclared but salvageable |
| 1 | Variant misdeclared (e.g., Cat 4 system written as full SDS, or Cat 5 system written as a thin reliance statement) AND/OR multiple sections missing |
| 0 | Document lacks recognisable DS structure; ad-hoc design narrative without sectioning |

**Required common sections (every DS):** YAML frontmatter with `parent_fs` block, H1 variant title, H2 system title, Document Control + Design Control block + Revision History + Definitions, § 1 Purpose, § 2 Scope, § 3 Architectural Overview, § N References, § N+1 DS → FS Traceability Matrix, § N+2 Design-level Risk Register, END marker.

**Variant-specific mandatory sections** — see METHODOLOGY § 2B.1 for the per-Cat table.

---

## Dimension 2 — Regulatory accuracy

**What's scored:** Do regulatory citations resolve to real, currently-effective documents? Are sub-section references correct? Does the Cat 5 DS correctly bind to IEC 62304 / IEC 81001-5-1 / similar SE standards (where applicable)? Does the Cat 1 DS correctly bind to CIS / BSI IT-Grundschutz / NIST SP 800-53?

| Score | Definition |
|---|---|
| 5 | All citations resolve and are correctly versioned; sub-section references correct; Cat-specific bindings (vendor manuals for Cat 4; software-engineering standards for Cat 5; infrastructure standards for Cat 1) all present and correct |
| 4 | All citations resolve; minor version-dating issues (e.g., "2018" instead of "2017") |
| 3 | All citations resolve; sub-section references mostly correct; 1–2 minor inaccuracies |
| 2 | 1 citation hallucinated OR multiple sub-section references wrong OR Cat-specific binding missing (e.g., Cat 5 DS lacking IEC 62304 reference where SaMD) |
| 1 | 2+ citations hallucinated |
| 0 | Wholesale fabricated regulatory framework |

**Known LLM failure modes to watch for** (in addition to the URS/FS failure modes — METHODOLOGY § 2A.1–2A.6):
- "IEC 62304 §§ 5.1.1 / 5.2 / 5.3 / 5.4 / 5.5 / 5.6 / 5.7 / 5.8" — verify each cited sub-section actually exists (IEC 62304 sub-sections are real but some commonly-fabricated ones are not).
- Fabricated vendor product configuration items (e.g., a "MassLynx Configuration Mode: Strict-GxP" — Strict-GxP is not a real MassLynx mode).
- Fabricated CIS Benchmark version numbers (e.g., "CIS Benchmark for Windows Server 2026 v1.0" before that benchmark publication).
- Fabricated OWASP LLM Top 10 entries (the 2025 release has 10 specific items; do not invent an 11th).
- "ISO/IEC 27001:2026" — verify against the actual ISO publication year (current: 2022).

---

## Dimension 3 — GAMP-category coherence (DS-variant specific)

**What's scored:** Does the DS variant (IDS / Cat-3 Reliance / CS / SDS) match the parent system's GAMP category, AND does the content within the variant match the variant's content rules (METHODOLOGY § 2B.4–2B.7)?

| Score | Definition |
|---|---|
| 5 | Variant correctly declared; content within the variant follows the variant's content rules exactly (Cat 4 CS uses per-CI rows with vendor-named CIs + default-vs-custom + justification; Cat 5 SDS includes all 8 sub-sections from § 2B.5; Cat 3 stays thin; Cat 1 stays topology-focused) |
| 4 | Variant correctly declared; content mostly follows content rules; minor scope creep (e.g., a Cat 4 DS that paraphrases the FS in § 4 instead of giving concrete CI values) |
| 3 | Variant correctly declared; content rules partially followed; some sections shallow |
| 2 | Variant correctly declared but content rules mis-applied (e.g., Cat 4 CS attempts to re-draw vendor source-code internals) |
| 1 | Variant correctly declared but content contradicts the variant's rules throughout |
| 0 | Variant misdeclared (wrong DS shape for the Cat) |

**Category-coherence invariants** (METHODOLOGY § 2B.1):

| Cat | Variant | Hard rules |
|---|---|---|
| Cat 1 | IDS | No IQ/OQ/PQ for the infra itself; cite infrastructure-qualification protocols by reference only |
| Cat 3 | Vendor-Design-Reliance Statement | Thin (≤ 300 L typical); vendor design docs catalogued; no re-drawing of vendor internals |
| Cat 4 | Configuration Specification (CS) | Per-CI rows with vendor-named CIs + default-vs-custom + justification + FS-IDs traced + Verified-by; vendor internals NOT redrawn; site-developed code (custom scripts/macros/reports) gets a mini-SDS sub-section |
| Cat 5 | Software Design Specification (SDS) | All 8 sub-sections (Architecture / Modules / Data / Algorithms / API / Security / Deployment / Module-Spec table); pseudocode allowed, source code not; IEC 62304 binding where SaMD |

---

## Dimension 4 — Design-item testability / verifiability

**What's scored:** Is every design item verifiable — i.e., does each row carry a `Verified by` reference (IQ / OQ / PQ test ID) AND a concrete chosen value or design statement that a tester can later check?

| Score | Definition |
|---|---|
| 5 | All design items verifiable; testability evident at row level (concrete vendor CI values, named test IDs, measurable thresholds); pseudocode in Cat 5 § 7 carries input/output type signatures + named edge cases |
| 4 | All design items verifiable; isolated weak phrasing |
| 3 | Most design items verifiable (≥ 80%); some adjective-stacking ("the system shall be properly configured") |
| 2 | Half or more design items have weak / untestable phrasing |
| 1 | Pervasive vague design ("the configuration shall be appropriate", "the module shall be well-designed") |
| 0 | No `Verified by` column; no concrete values; wholesale narrative without per-design-item structure |

**What strong testability looks like:**
- `DS-PART11-04 (CI): MassLynx > User Profiles > Approver Profile > CanApproveResults = True; Reviewer Profile > CanApproveResults = False; Analyst Profile > CanApproveResults = False; CanReviewResults = True (Reviewer + Approver only); Two-Step Approval Mode = Enabled. Justification: enforces SoD per 21 CFR Part 11 § 11.10(g). Default: Custom (vendor default is single-step approval). Verified by IQ-PART11-04 + OQ-PART11-04.` ✅
- `DS-ALG-02 (Cat 5): Bioavailability calculation = AUC(0-inf) / Dose; AUC computed by linear-up / log-down trapezoid per ICH M10 § 3 (chromatographic), extrapolation only when r² of terminal slope ≥ 0.9; numerical precision: 64-bit float; edge case: if last quantifiable sample fraction < 5% of Cmax, flag for SME review. Verified by OQ-ALG-02 + PQ-ALG-02.` ✅

**What weak testability looks like:**
- `DS-X: The configuration shall be set to enforce GxP compliance.` ❌ (no concrete value, no FS-ID, no Verified-by)
- `DS-Y: The module shall be designed using best practices.` ❌ (no module name, no responsibility, no interface)

---

## Dimension 5 — DS → FS traceability

**What's scored:** Does every DS-ID appear in DS § N+1 — DS → FS Traceability Matrix with a mapped FS-ID? Does every FS-ID in the parent FS get coverage in the DS (or get flagged as deferred / vendor-internal in the DS Revision History)?

| Score | Definition |
|---|---|
| 5 | All DS-IDs traced to ≥ 1 FS-ID in the matrix (no range compression); FS-ID coverage 100% OR all uncovered FS-IDs explicitly flagged in DS Revision History as deferred or vendor-internal; FS-IDs cited in the matrix all resolve in the parent FS |
| 4 | All DS-IDs traced; FS-ID coverage ≥ 95%; minor flagging gaps |
| 3 | All DS-IDs traced; FS-ID coverage ≥ 85% OR flagging coherent |
| 2 | Some DS-IDs missing from matrix; FS-ID coverage < 85% with no flagging rationale |
| 1 | Matrix present but largely empty OR range compression used (`DS-PART11-01..07 → FS-PART11-01..07`) |
| 0 | No DS → FS Traceability Matrix |

**Verification:** Count DS-IDs in the body (§ 4 onwards, before § N+1). Count rows in the matrix. Compute coverage. Cross-check 5 random FS-IDs from the parent FS — do they appear (either covered or flagged) in the DS?

---

## Dimension 6 — `shall` / `must` discipline + URS-ID-redrawing avoidance

**What's scored:** Is `shall` used where the DS describes a designed behaviour ("The configuration shall enforce..." / "The module shall expose...")? Is `must` reserved for constraints on downstream consumers / quoted regulator text? Does the DS body avoid citing URS-IDs directly (URS coupling is transitive via the FS — see METHODOLOGY § 2B.2)?

| Score | Definition |
|---|---|
| 5 | `shall`/`must` discipline maintained throughout; no URS-ID citations in DS body (only in `parent_urs` frontmatter block); descriptive design choices use indicative present where appropriate |
| 4 | Mostly correct; ≤ 2 `must` occurrences in design rows; ≤ 1 URS-ID cited in body |
| 3 | Mostly correct; 3–5 `must` occurrences in design rows; 2–3 URS-IDs cited in body |
| 2 | Half or more design rows use `must` OR multiple URS-ID citations in body |
| 1 | `must` and `shall` used interchangeably without discipline; URS-IDs cited throughout body |
| 0 | `should` used as normative verb (catastrophic) OR DS body re-implements URS-side traceability matrix |

**Verification:**
- `grep -inE "\bmust\b" <document>.md` — review each match.
- `grep -inE "URS-[A-Z0-9]+-[0-9]+" <document>.md` — count matches in body (frontmatter `parent_urs` block excluded).

---

## Pass / fail definition

| Outcome | Definition |
|---|---|
| **Pass — usable as first draft** | Dimension 1 ≥ 4 AND Dimension 2 ≥ 4 AND Dimension 3 ≥ 4 AND Dimension 5 ≥ 4 AND Dimensions 4, 6 ≥ 3 |
| **Conditional pass — first draft with mandatory edits** | All dimensions ≥ 3 but one or more of D1 / D2 / D3 / D5 = 3 |
| **Fail — rewrite required** | Any dimension = 0, or 2+ dimensions < threshold |

---

## Eval report template

For each scored document, the reviewer records:

```yaml
document_id: <slug>
parent_fs: <slug>
parent_urs: <slug>
parent_gamp_cat: <1|3|4|5>
ds_variant: <IDS|VendorRelianceStmt|CS|SDS>

reviewer_id: <blinded>
date: YYYY-MM-DD
time_min: <integer>

dimension_1_structural_completeness: <0-5>
dimension_2_regulatory_accuracy: <0-5>
dimension_3_gamp_cat_coherence: <0-5>
dimension_4_design_item_testability: <0-5>
dimension_5_ds_fs_traceability: <0-5>
dimension_6_shall_must_discipline: <0-5>

contamination_flag: <none|suspected|confirmed>
contamination_note: <empty unless flag set>

outcome: <pass|conditional_pass|fail>

dimension_notes:
  d1: "<free text>"
  d2: "<free text>"
  ...

global_note: "<one-paragraph summary of usability>"
```

---

## Aggregate report — DS-specific targets

Across the eval sample (typically 30 documents stratified across Cat 1 / 3 / 4 / 5):

| Metric | Target |
|---|---|
| Pass rate (full pass) | ≥ 55% (slightly lower than URS+FS target — DS is the most technical of the three artefacts) |
| Conditional-pass rate | ≤ 35% |
| Fail rate | ≤ 10% |
| Mean Dimension-2 score (regulatory accuracy) | ≥ 4.0 |
| Mean Dimension-3 score (GAMP-cat coherence) | ≥ 4.0 — non-negotiable for DS; getting the variant wrong invalidates the whole document |
| Mean Dimension-5 score (DS→FS traceability) | ≥ 4.0 |
| Inter-rater Cohen's κ (across all dimensions) | ≥ 0.60 |
| Contamination flags raised | 0 confirmed |

A model run that meets all aggregate thresholds is considered shipped. Below threshold → model is rolled back or pinned to a new fine-tune iteration.

---

## Eval sample stratification

For a 30-document DS eval:

- 6 Cat 4 lab instruments (CS — chromatography / spectroscopy / physical)
- 6 Cat 4 production control systems (CS — SCADA / DCS / MES / continuous mfg / tablet coater)
- 6 Cat 4 enterprise quality applications (CS — LIMS / ELN / eQMS / EDMS / RIM / Stability)
- 6 Cat 5 custom-developed (SDS — AI/ML Model Server / GenAI LLM Service / Custom CV / Custom Audit-Trail Workbench)
- 3 Cat 1 infrastructure (IDS — AD / Backup / NTP-related)
- 3 Cat 3 thin reliance statements (Karl Fischer / Particle Counter / Compendial Calculator)

---

## Reviewer profile (DS-specific)

The DS eval is performed by:

- 1 senior solution architect with ≥ 10 years of GxP CSV experience and direct exposure to FDA / EMA inspection — must have authored or reviewed at least 5 Cat 4 Configuration Specifications and 1 Cat 5 SDS in their career
- 1 QA reviewer at Quality Unit level with authorisation to approve design baselines in production at a regulated site
- For Cat 5 SDS scoring: 1 software-engineering reviewer with knowledge of IEC 62304 / IEC 81001-5-1 (where applicable) — optional third reviewer

Both primary reviewers are blind to which documents are model-generated versus which are corpus-template-derived.

Reviewers' identifications are blinded in the published eval report.

---

## What the eval cannot prove

The eval cannot prove a model-generated DS draft would survive a real GAMP audit or regulatory inspection. The only thing that proves that is: a Quality Unit reviewing the draft, a solution architect editing it for site-specific configuration values, the validation team running the planned IQ/OQ/PQ tests, and the inspector accepting the assembled validation package. The eval scores whether the DS is a credible *first-draft technical-design starting point* — that is the contract.

---

**Rubric version:** 1.1 · **Released:** 2026-05-16 · **License:** Apache 2.0 · **Changes from 1.0:** version bump to track the v1.1 corpus rename; no rubric-content changes (the 6 dimensions, the 0-5 scales, the pass/fail thresholds, the aggregate targets all carry forward unchanged).
