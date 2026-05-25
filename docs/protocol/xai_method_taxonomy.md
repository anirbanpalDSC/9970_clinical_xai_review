# XAI Method Taxonomy — Clinical Domain

**Issue:** #6
**Status:** Resolved 2026-05-23
**Feeds:** `XAI_Method` and `XAI_Scope` columns in extraction schema (Issue #10)

---

## Classification Dimensions

| Dimension | Definition | Values |
|-----------|------------|--------|
| Scope | Whether the explanation describes an individual prediction or the model as a whole | Local / Global / Both |
| Output type | The form of the explanation delivered to the user | Feature attribution / Example-based / Rule-based / Visual |
| Model-agnosticism | Whether the method can be applied to any model or requires access to specific internals | Model-agnostic / Model-specific / Both |
| Fidelity type | How the explanation relates to the model's actual computation | Exact game-theoretic / Exact gradient / Approximate surrogate / Perturbation-based |
| Clinical suitability | Known limitations relevant to clinical deployment — not a disqualifier, but flags to watch during extraction coding | Free text |

---

## Taxonomy Table

| Method | Scope | Output type | Model-agnostic | Fidelity type | Key citation | Clinical suitability issues |
|--------|-------|-------------|----------------|---------------|--------------|----------------------------|
| SHAP | Local (aggregable to global) | Feature attribution | Both — KernelSHAP: agnostic; TreeSHAP, DeepSHAP: model-specific | Exact game-theoretic (TreeSHAP); approximate surrogate (KernelSHAP) | Lundberg & Lee (2017) | Feature importance ≠ causality; correlated features distort attributions; TreeSHAP assumes feature independence; global SHAP beeswarm plots can obscure individual variation critical for clinical decisions |
| LIME | Local | Feature attribution | Model-agnostic | Approximate surrogate (local linear model) | Ribeiro et al. (2016) | Explanation instability across runs for same input; perturbation sampling can generate out-of-distribution inputs that mislead the surrogate; neighborhood kernel width is an arbitrary hyperparameter |
| Grad-CAM | Local | Visual (saliency map) | Model-specific (CNN / gradient-based architectures) | Exact gradient | Selvaraju et al. (2017) | Highlights image regions, not clinically labelled anatomical structures; spatial resolution is limited by the last convolutional layer; does not explain what feature property triggers the activation |
| Attention weights | Local (aggregable to global) | Feature attribution | Model-specific (transformer / attention architectures) | Exact (direct model component) | Vaswani et al. (2017); Jain & Wallace (2019) | Attention ≠ explanation — high attention weight does not reliably indicate causal feature importance (Jain & Wallace 2019). Papers claiming interpretability via attention alone should be flagged; attention is not faithful in the internal-mechanism sense |
| ANCHOR | Local | Rule-based (if-then predicates with precision guarantee) | Model-agnostic | Perturbation-based | Ribeiro et al. (2018) | Rules can be overly broad or trivially true; coverage-precision tradeoff is user-specified and arbitrary; may produce clinically uninterpretable combinations of features |
| Counterfactual explanations | Local | Example-based (what-if scenarios) | Model-agnostic | Perturbation-based (minimal-change search) | Wachter et al. (2017) | Actionability is constrained by which features can realistically change in a clinical pathway; multiple valid counterfactuals exist and selection is arbitrary; may suggest clinically impossible changes (e.g., alter a lab value to a physiologically implausible level) |
| Prototype / Criticism (MMD-critic) | Global | Example-based (representative and outlier cases) | Model-agnostic (operates on data distribution, not model internals) | Approximate (kernel density estimation) | Kim et al. (2016) | Prototypes may not correspond to clinically meaningful subtypes; criticism cases (outliers) can mislead clinicians unfamiliar with distributional reasoning; kernel choice affects which cases are selected |
| Rule extraction | Global (post-hoc) or Exact (inherently interpretable) | Rule-based | Both — post-hoc: model-agnostic; inherent: model IS the rules | Approximate surrogate (post-hoc) / Exact (inherently interpretable models: rule lists, scoring systems) | Rudin (2019); Lakkaraju et al. (2016) | Post-hoc rule extraction from neural networks has low faithfulness; Rudin (2019) argues only inherently rule-based models are acceptable for high-stakes clinical decisions. Code fidelity type separately: post-hoc rule extraction ≠ inherently interpretable model |

---

## Controlled Vocabulary for Extraction Schema

### XAI_Method values
Use these exact strings in `data/extraction/schema_v1.csv`:

`SHAP` | `LIME` | `GradCAM` | `Attention` | `ANCHOR` | `Counterfactual` | `Prototype` | `RuleExtraction` | `Other` | `Multiple`

If a paper uses multiple methods, enter `Multiple` and document individual methods in the Notes column.

### XAI_Scope values
`Local` | `Global` | `Both`

SHAP and attention are primarily local but are sometimes aggregated to global summaries. Code the scope as used in the paper, not as the method is theoretically capable of.

---

## Coding Notes

### Fidelity type and the Fidelity ≠ Faithfulness distinction
See `memos/terminology_instability.md` Part 1 (Rudin 2019 anchor). Approximate surrogate methods — LIME, ANCHOR, post-hoc rule extraction — can have high output-level fidelity on the training distribution while having low internal faithfulness on out-of-distribution inputs. Exact methods — TreeSHAP, Grad-CAM gradients — have higher faithfulness by construction because they trace the actual model computation.

### Attention weights
Do not code a paper as demonstrating faithful explanation solely because it reports attention weights. Apply the Jain & Wallace (2019) flag: attention weight magnitude is not a reliable indicator of feature importance. Papers that claim interpretability via attention without additional evaluation evidence should be coded `Eval_Type: Functionally-grounded` unless a human evaluation accompanies it.

### Inherently interpretable model vs post-hoc rule extraction
These use the same `RuleExtraction` method code but differ on fidelity type. Always record in Notes whether the rule-based model IS the classifier (inherently interpretable — Rudin sense) or is a post-hoc approximation of a separate black-box model.

---

## Methods to Add During Extraction (v1 gaps)

The 8 methods above are the named scope of Issue #6. Add rows here during extraction when additional methods are encountered:

| Method | Scope | Output type | Notes |
|--------|-------|-------------|-------|
| Integrated Gradients | Local | Feature attribution | Gradient-based, model-specific; stronger faithfulness guarantees than vanilla gradients; Sundararajan et al. (2017) |
| Explainable Boosting Machine (EBM / GA²M) | Global | Feature attribution (additive) | Inherently interpretable GAM with pairwise interactions; Rudin-compatible; increasingly common in clinical risk prediction; Lou et al. (2013) |
| DeepLIFT | Local | Feature attribution | Gradient-based variant; assigns contribution scores relative to a reference baseline; model-specific; Shrikumar et al. (2017) |
| TCAV | Global | Concept-based | Tests whether a learned concept influences predictions; used in radiology; Kim et al. (2018) |

---

## Link to Evaluation Type Taxonomy

The `Eval_Type` column in the extraction schema (Issue #10) requires a parallel taxonomy. Working framework from Doshi-Velez & Kim (2017):

| Eval_Type code | Definition | Ecological validity |
|----------------|------------|-------------------|
| `Application` | Real task, real clinicians in their practice role | Highest |
| `HumanGrounded` | Simplified task, real humans (may not be clinicians) | Moderate |
| `Functional` | Proxy metrics only — no human evaluation | Lowest |
| `Simulation` | Forward or counterfactual simulation tasks (see terminology_instability.md conflict log on Simulatability) | Depends on participant type |

Formalise and commit this taxonomy before piloting the extraction schema (Issue #5 or companion issue).
