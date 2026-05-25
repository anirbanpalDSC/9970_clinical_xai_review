# Tag Vocabulary — Clinical XAI Systematic Review (9970)

**Issue:** #13
**Status:** Resolved 2026-05-24
**Feeds:** `Tags` column in `data/extraction/schema_v1.csv`; in-text tagging of `memos/research_master_memo.md` and `memos/conceptual_distinctions.md`

---

## Usage Rules

1. **Syntax:** Tags use `#snake_case` lowercase. In free-text memos, embed inline (e.g., "This paper raises a #harking concern..."). In the extraction schema `Tags` column, separate multiple tags with semicolons: `#trust_calibration;#clinician_study`.
2. **Apply conservatively:** Tag only what the paper explicitly does or claims — not what it could have done. A paper must meet the `When to use` condition, not merely mention the concept.
3. **No minimum, no maximum:** A paper can carry one tag or ten. Completeness matters more than brevity.
4. **Schema and memo alignment:** Every tag applied in the schema `Tags` column should also appear in the corresponding extraction memo entry (and vice versa), so that schema-level retrieval and memo-level retrieval are consistent.
5. **Tag drift:** If a term changes meaning or a tag becomes ambiguous, add a note to the Changelog below — do not silently redefine.
6. **New tags:** Add to this vocabulary before using. Proposals go in `memos/decision_log.md`; add here once agreed. Do not introduce undocumented tags in the schema.

---

## Controlled Vocabulary

Tags are grouped thematically. Within each group, tags are ordered from most to least specific.

---

### Group A — Trust and Outcome Claims

These tags mark the nature of trust and outcome claims, directly feeding the `Trust_Claim`, `Trust_Only`, `Outcome_Claimed`, and `Outcome_Demonstrated` columns. See `memos/conceptual_distinctions.md` for the operational definitions behind this group.

| Tag | When to use | Schema column(s) |
|-----|-------------|-----------------|
| `#trust_calibration` | Paper provides evidence that clinician confidence tracks AI reliability — reliability anchor + trust measure + covariation evidence all present. Evidence goes beyond "trust improved." | `Trust_Claim: Calibrated` |
| `#explanation_plausibility` | Paper measures or claims that clinicians find explanations plausible, satisfying, or acceptable. Primary evidence is self-report (Likert, questionnaire). No reliability anchor required or present. | `Trust_Claim: Plausibility` or `Trust_Claim: Both` |
| `#trust_only` | Trust questionnaire is the **sole** evaluation of the XAI component — no decision quality or downstream outcome evidence alongside. | `Trust_Only: Yes` |
| `#fidelity` | Paper measures explanation faithfulness to the underlying model — AOPC, deletion/insertion curves, fidelity score, or faithfulness metrics. Distinct from decision quality: this evaluates the explanation's relationship to the model, not to clinical ground truth. | `Eval_Type: ProxyMetric` (subset) |
| `#outcome_gap` | Substantial gap between `Outcome_Claimed` and `Outcome_Demonstrated` — authors claim more than the data show. Use in addition to other trust/outcome tags. | `Trust_Claim: Both`; large gap between `Outcome_Claimed` and `Outcome_Demonstrated` |

---

### Group B — Evaluation Design and Realism

These tags characterise the study's evaluation design, mapping to columns in the Study Design, Eval Type, and Realism/EV sections of the schema.

| Tag | When to use | Schema column(s) |
|-----|-------------|-----------------|
| `#deployment` | XAI evaluated in active clinical deployment — real patients, real workflow, real EHR/PACS infrastructure. Corresponds to Realism Level 4. | `Realism_Level: 4` |
| `#workflow_realism` | Paper addresses integration of XAI into clinical workflow in any substantive way — even if not at deployment level. Use at Realism Level 3 or 4. | `Realism_Level: 3` or `4` |
| `#clinician_study` | Licensed clinicians participated in the evaluation. Use when `Clinician_Eval: Yes`. | `Clinician_Eval: Yes` |
| `#co_design` | A clinician was involved in designing or developing the XAI system — co-design, requirements elicitation, or iterative feedback during development. Use when `Clinician_Design: Yes`. | `Clinician_Design: Yes` |
| `#rct` | Study uses a randomised controlled trial design. | `Study_Design: RCT` |
| `#decision_quality` | Paper measures decision quality as an outcome — clinician accuracy, appropriateness, or error rate with vs without XAI, assessed against a clinical gold standard. | `Eval_Type` includes `DecisionQuality` |
| `#downstream_outcome` | Paper measures a patient or clinical outcome — mortality, diagnostic yield, treatment appropriateness, or a process measure with direct patient impact. | `Eval_Type` includes `DownstreamOutcome` |
| `#method_paper` | Paper presents the XAI method itself; clinical domain is illustrative only; no systematic evaluation of clinical utility. | `Study_Design: MethodPaper` |

---

### Group C — XAI Method

These tags characterise the explanation method used. They may be applied in addition to (not instead of) the `XAI_Method` schema column, because some tags group methods across schema vocabulary entries.

| Tag | When to use | Schema column(s) |
|-----|-------------|-----------------|
| `#feature_attribution` | Paper uses a feature attribution method: SHAP, LIME, Integrated Gradients, DeepLIFT, or any gradient-based attribution. Groups methods that answer "which input features contributed most to this prediction?" | `XAI_Method: SHAP` or `LIME` or `Other` (attribution subtype) |
| `#visual_saliency` | Paper uses a visual saliency method: Grad-CAM, Grad-CAM++, saliency maps, or attention visualisation applied to imaging data. | `XAI_Method: GradCAM` or `Attention` |
| `#counterfactual` | Paper uses counterfactual explanations: "what would need to change in the input for the prediction to change?" | `XAI_Method: Counterfactual` |
| `#attention_weights` | Paper uses raw attention weights as explanations. Apply in addition to `#visual_saliency` or `#feature_attribution` as appropriate. Requires special scrutiny: attention weight faithfulness is contested — tag every such paper for review during synthesis. | `XAI_Method: Attention` |
| `#inherently_interpretable` | Paper uses an inherently interpretable model (rule list, scoring system, decision tree, sparse linear model) — the explanation IS the model computation, not a post-hoc approximation. | `XAI_Method` may be `RuleExtraction` or `Other` |
| `#multi_method` | Paper evaluates or compares two or more XAI methods. | `XAI_Method: Multiple` |

---

### Group D — Methodological Quality

These tags flag methodological concerns or special characteristics that should be reviewed during quality assessment (Issue #20) and synthesis.

| Tag | When to use | Schema column(s) |
|-----|-------------|-----------------|
| `#harking` | Potential HARKing (Hypothesising After Results are Known) detected — paper's framing suggests conclusions were constructed post-hoc rather than from pre-registered hypotheses, or analyses appear selectively reported. Document the concern in `Notes`. | `Notes` |
| `#regulatory` | Paper explicitly mentions FDA clearance, CE marking, EU AI Act, or any regulatory compliance context for the XAI or underlying AI system. | `Notes` |
| `#terminology_conflict` | Paper uses a key term (interpretability, explainability, trust, fidelity, etc.) in a way that conflicts with the working definitions in `memos/terminology_instability.md` Part 1. Log the conflict in Part 2 of that document. | `Notes` |

---

## Tag × Schema Column Cross-Reference

Quick lookup: given a tag, which schema column(s) carry the same information?

| Tag | Redundant with column? | Notes |
|-----|----------------------|-------|
| `#trust_calibration` | `Trust_Claim: Calibrated` | Tag enables memo-level retrieval; column enables schema filtering |
| `#explanation_plausibility` | `Trust_Claim: Plausibility` or `Both` | Same |
| `#trust_only` | `Trust_Only: Yes` | Same |
| `#fidelity` | `Eval_Type: ProxyMetric` (partial) | ProxyMetric is broader; fidelity tags the specific faithfulness-metric subset |
| `#outcome_gap` | Gap between `Outcome_Claimed` / `Outcome_Demonstrated` | No dedicated column — tag provides retrieval |
| `#deployment` | `Realism_Level: 4` | Same |
| `#workflow_realism` | `Realism_Level: 3` or `4` | Same |
| `#clinician_study` | `Clinician_Eval: Yes` | Same |
| `#co_design` | `Clinician_Design: Yes` | Same |
| `#rct` | `Study_Design: RCT` | Same |
| `#decision_quality` | `Eval_Type` includes `DecisionQuality` | Same |
| `#downstream_outcome` | `Eval_Type` includes `DownstreamOutcome` | Same |
| `#method_paper` | `Study_Design: MethodPaper` | Same |
| `#feature_attribution` | `XAI_Method: SHAP` / `LIME` / attribution subtype | Groups across schema vocabulary entries |
| `#visual_saliency` | `XAI_Method: GradCAM` / `Attention` | Same |
| `#counterfactual` | `XAI_Method: Counterfactual` | Same |
| `#attention_weights` | `XAI_Method: Attention` | Subset with specific scrutiny flag |
| `#inherently_interpretable` | `XAI_Method: RuleExtraction` or `Other` | Schema column insufficient alone — tag clarifies |
| `#multi_method` | `XAI_Method: Multiple` | Same |
| `#harking` | `Notes` | No dedicated column — tag provides retrieval |
| `#regulatory` | `Notes` | Same |
| `#terminology_conflict` | `Notes` | Same |

Tags that are redundant with a schema column still provide value for memo-level retrieval, where the schema is not consulted. Both layers should be populated.

---

## Memo Tagging Convention

In `memos/research_master_memo.md` and other memo files, embed tags in the sentence where the relevant claim is described:

> "The paper uses SHAP on a deep EHR model and reports a trust questionnaire improvement, with no fidelity evaluation #explanation_plausibility #trust_only. Authors claim the explanations facilitate calibrated trust in their conclusion #outcome_gap."

Tags in memos from before 2026-05-24 (prior to this vocabulary) are not retroactively required — the tag system applies from this date forward.

---

## Changelog

| Date | Change |
|------|--------|
| 2026-05-24 | v1. 21 tags across four groups. Extends Issue #13 seed vocabulary of 11 tags. Added: `#outcome_gap`, `#co_design`, `#rct`, `#decision_quality`, `#downstream_outcome`, `#method_paper`, `#attention_weights`, `#inherently_interpretable`, `#multi_method`, `#terminology_conflict`. |
