# PubMed Search String v1 — Clinical XAI Systematic Review (9970)

**Issue:** #15
**Status:** Draft v1 — ready for test run
**Database:** MEDLINE via PubMed
**Date range filter:** 2015/01/01 – 2024/12/31
**Language filter:** English

---

## Design Rationale

The string uses a **two-concept AND structure** rather than three:

- **Concept A — XAI / Interpretability** (the intervention, from `xai_method_taxonomy.md`)
- **Concept B — Clinical / Medical Context** (the domain, from Gate 1 of `inclusion_boundary.md`)

A separate "AI/ML system present" check is deliberately **not** layered in as a third concept: every Concept A term (explainable AI, interpretable machine learning, SHAP, LIME, Grad-CAM, attention, etc.) already presupposes an AI/ML system by definition — adding a redundant generic-AI requirement only risks excluding papers that name a specific model ("XGBoost," "ResNet") rather than saying "machine learning."

Gate 2 (individual patient decision) and Gate 3 (clinician in the loop) are **not** encoded as search terms. These are eligibility properties that rarely appear as distinguishing vocabulary in titles/abstracts — encoding them would cost recall without buying precision (a paper passing Gates 1 may still describe Gate 2/3 only in its Methods section). They remain screening-stage filters, applied during title/abstract and full-text review per `inclusion_boundary.md`.

This mirrors the standard sensitivity-favouring design for systematic review searches: cast a wide net on the two concepts that reliably appear in abstracts, let the screening criteria do the precision work.

---

## Concept A — XAI / Interpretability

```
("explainable artificial intelligence"[tiab] OR "explainable AI"[tiab] OR "XAI"[tiab]
OR "interpretable machine learning"[tiab] OR "interpretability"[tiab] OR "model interpretability"[tiab]
OR "explainability"[tiab] OR "explainable model*"[tiab]
OR "SHAP"[tiab] OR "Shapley additive explanation*"[tiab] OR "Shapley value*"[tiab]
OR "LIME"[tiab] OR "local interpretable model-agnostic"[tiab]
OR "Grad-CAM"[tiab] OR "gradient-weighted class activation"[tiab] OR "class activation map*"[tiab]
OR "saliency map*"[tiab] OR "attention map*"[tiab] OR "attention weight*"[tiab] OR "attention mechanism*"[tiab]
OR "counterfactual explanation*"[tiab]
OR "feature attribution"[tiab] OR "feature importance"[tiab]
OR "rule extraction"[tiab] OR "decision rule*"[tiab]
OR "prototype-based explanation*"[tiab]
OR "interpretable AI"[tiab] OR "interpretable artificial intelligence"[tiab]
OR "black box"[tiab] OR "black-box"[tiab] OR "explainable deep learning"[tiab])
```

Source: every method named in `xai_method_taxonomy.md` (SHAP, LIME, Grad-CAM, Attention, ANCHOR — covered by "decision rule*"/"rule extraction", Counterfactual, Prototype, Rule extraction) plus the umbrella terminology terms from the foundational papers (Lipton, Doshi-Velez, Adadi, Arrieta).

---

## Concept B — Clinical / Medical Context

```
("clinical decision support"[tiab] OR "clinical decision support system*"[tiab] OR "CDSS"[tiab]
OR "computer-aided diagnos*"[tiab] OR "computer aided diagnos*"[tiab]
OR "diagnostic algorithm*"[tiab] OR "predictive model*"[tiab] OR "risk prediction model*"[tiab]
OR "clinical"[tiab] OR "clinician*"[tiab] OR "physician*"[tiab] OR "radiolog*"[tiab]
OR "patholog*"[tiab] OR "nurse*"[tiab] OR "diagnosis"[tiab] OR "diagnostic"[tiab]
OR "prognosis"[tiab] OR "treatment"[tiab] OR "patient care"[tiab] OR "hospital*"[tiab]
OR "Decision Support Systems, Clinical"[Mesh] OR "Physicians"[Mesh]
OR "Clinical Decision-Making"[Mesh] OR "Diagnosis, Computer-Assisted"[Mesh]
OR "Patient Care"[Mesh])
```

**Revision note (2026-06-07):** v1 originally nested an AI/ML "technology" sub-block inside Concept B, ANDed against the clinical-context sub-block — making the overall query a 3-way intersection (XAI term AND generic-AI term AND clinical term). That returned only 9 hits, signalling over-constraint: papers that name a specific model ("XGBoost," "ResNet," "random forest") rather than saying "machine learning" or "artificial intelligence" were being filtered out before the clinical-context check ever ran. The technology sub-block was redundant — every Concept A term (explainable AI, interpretable machine learning, SHAP, LIME, Grad-CAM, etc.) already implies an AI/ML system by definition. Removed it; Concept B is now a single flat OR block of clinical-context terms only, restoring the genuine two-concept design described in the rationale above.

---

## Full Combined String

```
(Concept A) AND (Concept B)

AND ("2015/01/01"[Date - Publication] : "2024/12/31"[Date - Publication])
AND English[Language]
```

Paste-ready single-line version (PubMed search box):

```
("explainable artificial intelligence"[tiab] OR "explainable AI"[tiab] OR "XAI"[tiab] OR "interpretable machine learning"[tiab] OR "interpretability"[tiab] OR "model interpretability"[tiab] OR "explainability"[tiab] OR "explainable model*"[tiab] OR "SHAP"[tiab] OR "Shapley additive explanation*"[tiab] OR "Shapley value*"[tiab] OR "LIME"[tiab] OR "local interpretable model-agnostic"[tiab] OR "Grad-CAM"[tiab] OR "gradient-weighted class activation"[tiab] OR "class activation map*"[tiab] OR "saliency map*"[tiab] OR "attention map*"[tiab] OR "attention weight*"[tiab] OR "attention mechanism*"[tiab] OR "counterfactual explanation*"[tiab] OR "feature attribution"[tiab] OR "feature importance"[tiab] OR "rule extraction"[tiab] OR "decision rule*"[tiab] OR "prototype-based explanation*"[tiab] OR "interpretable AI"[tiab] OR "interpretable artificial intelligence"[tiab] OR "black box"[tiab] OR "black-box"[tiab] OR "explainable deep learning"[tiab])
AND
AND
("clinical decision support"[tiab] OR "clinical decision support system*"[tiab] OR "CDSS"[tiab] OR "computer-aided diagnos*"[tiab] OR "computer aided diagnos*"[tiab] OR "diagnostic algorithm*"[tiab] OR "predictive model*"[tiab] OR "risk prediction model*"[tiab] OR "clinical"[tiab] OR "clinician*"[tiab] OR "physician*"[tiab] OR "radiolog*"[tiab] OR "patholog*"[tiab] OR "nurse*"[tiab] OR "diagnosis"[tiab] OR "diagnostic"[tiab] OR "prognosis"[tiab] OR "treatment"[tiab] OR "patient care"[tiab] OR "hospital*"[tiab] OR "Decision Support Systems, Clinical"[Mesh] OR "Physicians"[Mesh] OR "Clinical Decision-Making"[Mesh] OR "Diagnosis, Computer-Assisted"[Mesh] OR "Patient Care"[Mesh])
AND ("2015/01/01"[Date - Publication] : "2024/12/31"[Date - Publication])
AND English[Language]
```

---

## Known Limitations / Things to Watch in Validation (Issue #16)

1. **"Black box" is a noisy term** — also used in aviation, automotive, and general computing contexts. Likely contributes false positives but is retained because some clinical XAI papers use "opening the black box" framing in titles (e.g., Adadi & Berrada). Monitor its precision contribution during recall validation; consider dropping if it inflates irrelevant hits disproportionately.
2. **"ANCHOR" intentionally omitted as a bare term** — too short and ambiguous (matches anatomical anchors, surgical anchors). Coverage relies on "decision rule*" and "rule extraction" instead; if seed papers using ANCHOR are missed in validation, add `"anchor explanation*"[tiab]` or `"anchors LIME"[tiab]` as a targeted addition.
3. **Attention-related terms may over-match** — "attention" is common in clinical psychology/behavioural literature ("patient attention", "attention deficit"). The AND with Concept B should suppress most of this, but check false-positive rate during validation.
4. **MeSH terms lag new technology** — "Artificial Intelligence"[Mesh] and "Machine Learning"[Mesh] may not yet be indexed on very recent papers (indexing lag ~6 months to 2 years). The [tiab] terms compensate for this; do not rely on MeSH alone.
5. **No drug/device brand names included** — by design (Gate 1 excludes drug discovery; consumer wearables are excluded at Gate 1 unless clinically overseen).

---

## Next Steps

1. Run this string in PubMed; record total hit count here.
2. Issue #16 — validate recall against the seed paper set (the same papers used for EV rubric and quality rubric piloting): confirm all seed papers are retrievable by this string. If any are missed, diagnose which concept block failed to match and revise.
3. Log the final hit count and any revisions in `memos/decision_log.md` before the search is executed for record (the logged string becomes the version reported in PRISMA Identification).
4. Translate to other databases (Embase, CINAHL, IEEE Xplore, ACM Digital Library) per Issue #22 — syntax differs (Emtree vs MeSH, field tag conventions).

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1 | 2026-06-07 | Initial draft. Two-concept AND structure (XAI terms AND clinical-AI terms). Ready for test run and recall validation against seed papers. Issue #15. |
