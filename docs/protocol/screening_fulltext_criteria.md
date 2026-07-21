# Full-Text Screening Criteria and Exclusion Taxonomy

**Issue:** #18
**Status:** Resolved 2026-05-26
**Applies to:** Full-text screening phase only
**Upstream document:** `docs/protocol/inclusion_boundary.md` (Issue #7 — three-gate inclusion boundary)
**Output file:** `data/screening/prisma_counts.csv`

---

## 1. Purpose

Title/abstract screening applies the three-gate inclusion boundary conservatively: when doubt exists, include for full-text review. Full-text screening applies all criteria strictly, adds criteria that cannot be confirmed from title/abstract alone, and requires documented exclusion reasons for PRISMA reporting.

This document defines:
1. What must be confirmed at full-text before a paper proceeds to extraction
2. The controlled exclusion reason taxonomy (E1–E6)
3. Decision rules for borderline cases
4. The piloting protocol before full-text screening begins

---

## 2. Relationship to Upstream Criteria

The three gates from `docs/protocol/inclusion_boundary.md` remain in effect at full-text. Gate confirmation is typically straightforward at this stage because the abstract already passed. Additional full-text criteria address aspects that cannot be confirmed from title/abstract alone:

| Criterion | Title/abstract screening | Full-text screening |
|-----------|--------------------------|---------------------|
| Gate 1 — Clinical domain | Applied loosely | Applied strictly |
| Gate 2 — Individual patient decision | Applied loosely | Applied strictly |
| Gate 3 — Clinician in loop | Applied loosely | Applied strictly |
| XAI component confirmed (F2) | Not confirmable | Applied strictly |
| XAI evaluation present (F3) | Not confirmable | Applied strictly |
| Publication type (F5) | Applied loosely | Applied strictly |
| Sufficient extraction detail (F4) | Not applicable | Applied strictly |
| Duplicate check (F6/E6) | Not applicable | Applied strictly |

---

## 3. Full-Text Inclusion Criteria

A paper proceeds to extraction if and only if it satisfies ALL of the following criteria.

### F1 — Three gates confirmed

All three gates from `docs/protocol/inclusion_boundary.md` are satisfied as confirmed in the full text, not just the abstract. Re-read the Methods section to verify the clinical domain, decision target, and clinician involvement claims.

### F2 — XAI component confirmed

The paper describes at least one identifiable XAI method — from the controlled vocabulary in `docs/protocol/xai_method_taxonomy.md`, or a method that would be coded `Other` — applied to a clinical AI system.

Interpretability achieved through model choice alone (logistic regression, decision tree, linear model) qualifies only if:
- The paper explicitly frames the model's interpretability as its XAI/interpretability contribution, AND
- The paper evaluates the interpretability component — not merely reports model coefficients or feature weights in a table.

### F3 — XAI evaluation present

The paper reports at least one evaluation of the XAI component, however minimal. Acceptable evaluation forms:
- Proxy metric applied to XAI outputs (fidelity, faithfulness, sparsity, stability) — coded `Eval_Type: ProxyMetric`
- Human-participant study of any kind — coded with appropriate `Eval_Type`
- Deployment study measuring real outcomes — coded `Eval_Type: DownstreamOutcome`

**MethodPaper exception:** Papers that present a new XAI method and use a clinical domain as a demonstration case, without a systematic evaluation of clinical utility, are included but coded `Study_Design: MethodPaper` and `Eval_Type: None`. The XAI method must be the stated primary contribution; a post-hoc SHAP figure in a clinical prediction paper does not qualify.

### F4 — Sufficient extraction detail

The full text is available in English and provides enough methodological detail to fill the mandatory schema fields: `Domain`, `XAI_Method`, `XAI_Scope`, `Study_Design`, `Realism_Level`, and `Trust_Claim`. Papers where key Methods content is locked behind a separate supplementary file that is unavailable, or where the paper is in conference abstract format with no full proceedings, are excluded via E5.

### F5 — Primary empirical study

Review articles, systematic reviews, editorials, opinion pieces, commentaries, protocol-only papers (no results), and book chapters are excluded via E4. Conference papers are included if a full Methods and Results paper is available; abstract-only conference submissions are excluded.

---

## 4. Exclusion Reason Taxonomy

When a full-text paper is excluded, assign one primary exclusion reason from the table below. If multiple reasons apply, assign the highest-priority code (lowest number).

| Code | Label | Definition | Priority |
|------|-------|------------|----------|
| `E1` | Not clinical AI application | Fails Gate 1, Gate 2, or Gate 3 on full-text review. Covers: administrative AI, consumer-facing health AI, drug discovery, population-only analytics, or no clinician in the decision loop. | 1 (highest) |
| `E2` | No XAI component | The paper evaluates a clinical AI system but applies no XAI method meeting criterion F2. Includes: model performance evaluation with no explanation output, SHAP/LIME mentioned in a single sentence without evaluation, feature importance from the model itself presented without XAI framing. | 2 |
| `E3` | XAI not evaluated | An XAI method is applied and described but is not evaluated in any form meeting F3. The XAI output is a figure or supplementary table only, with no proxy metric, no human evaluation, and no authorial claim that the XAI component is being evaluated. Distinct from MethodPaper (see F3 exception). | 3 |
| `E4` | Wrong publication type | Review article, systematic review, editorial, opinion piece, commentary, protocol paper without results, book chapter, or conference abstract without full proceedings. Applies even if substantive XAI content is present. | 4 |
| `E5` | Insufficient extraction detail | Paper passes F1–F3 but provides insufficient methodological detail to fill mandatory schema fields. Document which specific mandatory fields cannot be filled in `data/screening/fulltext_exclusions.csv`. | 5 |
| `E6` | Duplicate report | A different report of a study already included or being processed (e.g., conference version of an included journal paper, same dataset with minor extension). If both reports add extractable data not present in the other, include both and cross-link via `Notes`. If one report is a strict subset, include only the more complete report. | 6 (lowest) |

### E3 vs MethodPaper — critical distinction

| Scenario | Code | Reason |
|----------|------|--------|
| "We propose XAI-Net for chest X-ray diagnosis and evaluate its faithfulness and clinician acceptance across three hospitals." | **Include as MethodPaper** | XAI is the stated contribution; the paper evaluates it |
| "We trained XGBoost for ICU mortality prediction (AUROC 0.84). Figure 3 shows SHAP feature importance." | **Exclude E3** | XAI is incidental decoration; no evaluation of the explanation |
| "We use LIME to explain our sepsis prediction model. Clinicians rated explanations on a 5-point scale." | **Include** | XAI is evaluated (human-participant rating) |
| "We present a logistic regression model for readmission risk. Odds ratios are reported in Table 2." | **Exclude E2** | No XAI method; model coefficients are not XAI |

---

## 5. Borderline Decision Rules

### Rule 1 — Inherently interpretable models
Model coefficients, feature importance from tree-based models, and attention weights reported without evaluation do not constitute an XAI contribution meeting F2. Apply the MethodPaper exception only if: (a) the paper's stated primary contribution is the interpretable design, and (b) the paper includes deliberate evaluation of the interpretability component beyond reporting the model's outputs.

### Rule 2 — Mixed clinical and non-clinical participants
If a paper uses a mixed participant pool (clinicians plus lay participants), Gate 3 is met if at least some clinicians participate in a role that mirrors the real clinical decision workflow. Code `Participant_Type: MixedClinical` and document the breakdown in `Notes`.

### Rule 3 — Proxy-metric-only evaluations
Papers reporting only computational proxy metrics (fidelity, faithfulness, sparsity, stability) with no human participants are in scope. Code `Eval_Type: ProxyMetric`, `N_Participants: 0`, `Participant_Type: None`. Do not apply E3.

### Rule 4 — XAI used internally for model selection
XAI used only to justify model selection or architecture choices (e.g., "SHAP confirms our model uses clinically plausible features — we chose this model over XGBoost on this basis") without integration into a clinical workflow or evaluation of clinician interaction is borderline. Apply E2 if the XAI output is never presented to clinicians in any described evaluation; include if the XAI output is part of any described clinician interaction.

### Rule 5 — Duplicate reports
Before applying E6, search for the same corresponding author and overlapping dataset across the included and pending papers. Log both titles and the resolution rationale in `memos/decision_log.md`. If uncertain, include both and flag for second reviewer.

### Rule 6 — Non-English supplementary material
If key Methods detail is in a non-English supplementary document that cannot be machine-translated reliably, apply E5. Document the field gaps.

### Rule 7 — Review/wrong-publication-type vs. Gate failure
Review articles, editorials, commentaries, protocol-only papers, and abstract-only submissions will trivially fail Gates 1–3 (Section 3, F1) simply by not themselves deploying, testing, or implementing a clinical AI system — this is a consequence of their format, not a substantive finding about clinical domain fit. If a paper's Gate 1–3 failures stem solely from its being this kind of publication, code **E4**, not E1, even though the numeric tie-break rule (Section 4) would otherwise select E1 as the lower-numbered code. Reserve E1 for primary empirical studies that fail on substantive domain, decision-point, or clinician-involvement grounds despite being an eligible study type. This rule is an explicit exception to the numeric priority tie-break, added because strict application would make E4 practically unusable for its intended purpose (PRISMA-reportable review/wrong-publication-type exclusions).

If a review also contains a genuine embedded primary study (e.g., a novel analysis presented alongside the review), evaluate that embedded component against F1–F5 separately.

---

## 6. Piloting Protocol

Before full-text screening begins on the full included pool:

1. Two reviewers independently apply these criteria to 10 full texts drawn from the included pool after title/abstract screening.
2. Record inclusion decision and, for excluded papers, the exclusion code per paper.
3. Calculate Cohen's kappa on the binary include/exclude decision across the 10 papers. Target: κ > 0.70.
4. Resolve disagreements by discussion; document resolutions in `memos/decision_log.md`.
5. If κ < 0.70 after the first pilot: identify the criterion causing most disagreements, revise the wording or add a decision rule, then pilot again on 5 additional papers.
6. Do not proceed to full screening until κ > 0.70 is confirmed.

**Pilot paper selection:** Draw 10 papers spanning at least three clinical domains. Deliberately include at least one paper that is borderline on each of the most contested distinctions: F2 (inherently interpretable models), F3 / E3 (SHAP-as-figure vs MethodPaper), and E4 (conference papers).

---

## 7. PRISMA Reporting

Exclusion reasons must be reported per-paper in the PRISMA flow diagram (full-text excluded, with reasons counted by code). Two files support this:

| File | Purpose |
|------|---------|
| `data/screening/prisma_counts.csv` | Aggregate counts per PRISMA stage; updated after each screening phase |
| `data/screening/fulltext_exclusions.csv` | Paper-level log of excluded full texts; created at screening time |

Required columns for `data/screening/fulltext_exclusions.csv` (create at screening time):

| Column | Type | Description |
|--------|------|-------------|
| `PaperID` | string | `LASTNAME_YEAR` identifier |
| `Title` | string | Full paper title |
| `Zotero_Key` | string | Zotero item key |
| `Exclusion_Code` | categorical | `E1` / `E2` / `E3` / `E4` / `E5` / `E6` |
| `Exclusion_Notes` | string | Brief rationale; mandatory fields missing (for E5); cross-reference (for E6) |

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1 | 2026-05-26 | Initial criteria. Five inclusion criteria (F1–F5), six exclusion codes (E1–E6), six borderline rules, piloting protocol. Issue #18. |
| v1.1 | 2026-07-10 | Added Rule 7 (Review/wrong-publication-type vs. Gate failure), an explicit exception to the numeric E-code tie-break: papers that fail Gates 1–3 solely because they are reviews/editorials/protocol-only/abstract-only papers are coded E4, not E1, since E1 would otherwise make E4 structurally unusable. Surfaced during the 10-paper full-text pilot (`rayyan-601300218`). See `memos/decision_log.md`, 2026-07-10. |
