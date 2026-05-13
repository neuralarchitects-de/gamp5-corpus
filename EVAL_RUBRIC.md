# Evaluation Rubric — Day-30 Human-QA Review of Fine-Tuned Model Output

**Audience:** human reviewers (senior validation engineer + QA reviewer) scoring documents produced by the Qwen 3 7B model fine-tuned on this corpus. Released alongside the Day-30 model.

**License:** Apache 2.0 (the rubric is engineering work, not data).

---

## What's being evaluated

The model output is a User Requirements Specification (or Functional Specification) for a regulated computer system. The model is given a brief intended-use prompt (e.g., "Generate a URS for a Cat 4 dissolution apparatus computer system used in pharmaceutical QC dissolution testing") and produces a full document.

The rubric scores whether the model's output is a **credible first draft** that a competent validation engineer can iterate on — not whether the output is a regulatorily-signable URS. See `METHODOLOGY.md` § 4.1 for the philosophy.

---

## Scoring instructions

For each document, score each of 6 dimensions on a 0–5 scale. Mark the time taken (in minutes) to review. Blind-flag any document that appears to plagiarise from a real client URS (this is a contamination check, not a pass/fail dimension).

Inter-rater reliability: 2 reviewers score the same sub-sample of 6 documents independently. Calculate Cohen's κ for each dimension. κ ≥ 0.60 (substantial agreement) is the threshold for the rubric being usable; below that, the rubric needs sharpening.

---

## Dimension 1 — Structural completeness

**What's scored:** Does the document carry all GAMP 5 canonical sections in the right order?

| Score | Definition |
|---|---|
| 5 | All sections present and ordered; § 5 broken into 8+ sub-sections by domain; Appendix A — Traceability Seed present with full URS-ID → FS-ID → test mapping |
| 4 | All sections present and ordered; § 5 broken into 5+ sub-sections; Traceability Seed present |
| 3 | All sections present; some § 5 collapse to combined section but content covered |
| 2 | 1–2 sections missing or out of order |
| 1 | Multiple sections missing or significantly out of order |
| 0 | Document lacks recognisable URS structure |

**Required sections (each must be present):** Document Control, Definitions, § 1 Purpose, § 2 Scope, § 3 System Description and Intended Use, § 4 User Roles, § 5 User Requirements, § 6 Acceptance Criteria, § 7 Constraints, § 8 Assumptions, § 9 Risks, § 10 References, Appendix A.

---

## Dimension 2 — Regulatory accuracy

**What's scored:** Do regulatory citations resolve to real, currently-effective documents? Are sub-section references correct?

| Score | Definition |
|---|---|
| 5 | All citations resolve and are correctly versioned; sub-section references correct; category-bound citations match the declared GAMP category |
| 4 | All citations resolve; minor version-dating issues (e.g., "2018" instead of "2017") |
| 3 | All citations resolve; sub-section references mostly correct; 1–2 minor inaccuracies |
| 2 | 1 citation hallucinated OR multiple sub-section references wrong |
| 1 | 2+ citations hallucinated |
| 0 | Wholesale fabricated regulatory framework |

**Verification method:** Reviewer checks each citation in § 10 (References) against the maintained list of known-real regulatory documents (see `regulatory_source_pack/` in the repository). Hallucinations are catastrophic — they break the corpus's credibility commitment.

**Known LLM failure modes to watch for:**
- "FDA Guidance on Pharmaceutical Quality Engineering" (no such guidance exists)
- "21 CFR Part 11, Section 11.55" (Part 11 has no § .55)
- "ICH Q14 (R3)" (Q14 has no R3 revision as of corpus release)
- "EU Annex 11, Article 18" (Annex 11 has 17 numbered clauses, no Article 18)
- "GAMP 5 (3rd Edition, 2024)" (3rd Edition does not exist)
- Adjective swaps: "EU AI Act 2024" framed as "EU AI Act 2026" or "EU AI Regulation 2024"

---

## Dimension 3 — GAMP categorisation coherence

**What's scored:** Does the declared GAMP category drive the validation depth and structure?

| Score | Definition |
|---|---|
| 5 | Category declared; structure matches; category-specific concerns explicitly addressed (e.g., Cat 5 includes custom SDLC + change-control-plan + per-version validation) |
| 4 | Category declared; structure matches; category-specific concerns mostly addressed |
| 3 | Category declared; structure matches; minor category-specific gaps |
| 2 | Category declared but structure inconsistent (e.g., Cat 4 declared but custom-development requirements present) |
| 1 | Category declared but contradicted throughout |
| 0 | No category declaration |

**Category-structure invariants:**

| Category | Required structural elements |
|---|---|
| Cat 1 (Infrastructure) | No IQ/OQ/PQ acceptance; infrastructure-qualification protocol references; configuration-management focus |
| Cat 3 (Non-Configurable COTS) | IQ + OQ acceptance; no PQ for the COTS itself; vendor-SDLC reliance section |
| Cat 4 (Configured Products) | IQ + OQ + PQ acceptance; configuration-specification section; vendor + site responsibility split |
| Cat 5 (Custom / Site-Developed) | IQ + OQ + PQ acceptance; custom-development-lifecycle section; site-SDLC documentation; per-version validation evidence |

---

## Dimension 4 — Requirement testability

**What's scored:** Is every requirement a verifiable `shall`-clause with a clear test target?

| Score | Definition |
|---|---|
| 5 | All requirements verifiable; testability evident at line level (numeric thresholds, specific verbs, named artefacts) |
| 4 | All requirements verifiable; isolated weak phrasing |
| 3 | Most requirements verifiable (≥ 80%); some adjective-stacking |
| 2 | Half or more requirements have weak / untestable phrasing |
| 1 | Pervasive vague requirements ("system shall be robust", "system shall be reliable") |
| 0 | No `shall`-clauses or wholesale untestable narrative |

**What strong testability looks like:**
- `URS-PERF-02: Chromatographic processing of a 50-injection sequence shall complete within 15 minutes on the dedicated workstation.` ✅ (numeric + scoped + measurable)
- `URS-BAK-02: A documented restore test shall be performed quarterly by the System Administrator with witness from QC.` ✅ (frequency + responsible role + verification mechanism)

**What weak testability looks like:**
- `URS-X: The system shall be reliable and performant.` ❌ (adjective-stacking, no measurable threshold)
- `URS-Y: The system shall provide a good user experience.` ❌ (subjective, no test target)

---

## Dimension 5 — Traceability

**What's scored:** Does every URS-ID appear in Appendix A — Traceability Seed with a planned FS-ID and IQ/OQ/PQ test reference?

| Score | Definition |
|---|---|
| 5 | All URS-IDs traced; FS pair (if generated) cross-references correctly; orphan requirements explicitly flagged |
| 4 | All URS-IDs traced; FS cross-reference present but with minor gaps |
| 3 | ≥ 80% of URS-IDs traced; FS cross-reference present |
| 2 | < 80% traced; Appendix A incomplete |
| 1 | Appendix A present but largely empty |
| 0 | No Appendix A; no traceability seed |

**Verification:** Count URS-IDs in § 5. Count entries in Appendix A. Compute coverage percentage.

---

## Dimension 6 — `shall`/`must` discipline

**What's scored:** Is `shall` used for system requirements; `must` reserved for constraints on downstream consumers / processes?

| Score | Definition |
|---|---|
| 5 | Discipline maintained throughout; `must` appears only in clearly-scoped consumer / process constraints |
| 4 | Mostly correct; ≤ 2 `must` occurrences in system requirements |
| 3 | Mostly correct; 3–5 `must` occurrences in system requirements |
| 2 | Half or more system requirements use `must` |
| 1 | `must` and `shall` used interchangeably without discipline |
| 0 | `should` used as normative verb (catastrophic) |

**Verification:** `grep -in "\bmust\b" <document>.md` — review each match.

---

## Pass / fail definition

| Outcome | Definition |
|---|---|
| **Pass — usable as first draft** | Dimension 1 ≥ 4 AND Dimension 2 ≥ 4 AND Dimension 5 ≥ 4 AND Dimensions 3, 4, 6 ≥ 3 |
| **Conditional pass — first draft with mandatory edits** | All dimensions ≥ 3 but one or more of D1 / D2 / D5 = 3 |
| **Fail — rewrite required** | Any dimension = 0, or 2+ dimensions < threshold |

---

## Eval report template

For each scored document, the reviewer records:

```yaml
document_id: <slug>
reviewer_id: <blinded>
date: YYYY-MM-DD
time_min: <integer>

dimension_1_structural_completeness: <0-5>
dimension_2_regulatory_accuracy: <0-5>
dimension_3_gamp_category_coherence: <0-5>
dimension_4_requirement_testability: <0-5>
dimension_5_traceability: <0-5>
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

## Aggregate report

Across the 30-document sample:

| Metric | Target |
|---|---|
| Pass rate (full pass) | ≥ 60% |
| Conditional-pass rate | ≤ 30% |
| Fail rate | ≤ 10% |
| Mean Dimension-2 score (regulatory accuracy) | ≥ 4.0 |
| Inter-rater Cohen's κ (across all dimensions) | ≥ 0.60 |
| Contamination flags raised | 0 confirmed |

A model run that meets all six aggregate thresholds is considered shipped. Below threshold → model is rolled back or pinned to a new fine-tune iteration.

---

**Rubric version:** 1.0 · **Released:** 2026-05-12 · **License:** Apache 2.0
