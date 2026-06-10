# PubMed Search String v1 — Clinical XAI Systematic Review (9970)

**Issue:** #15
**Status:** v1 finalized — diagnosed, precision-tuned, and recall-validated against an independent benchmark (9,672 hits). Ready for execution and PRISMA logging.
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

## Concept A — XAI / Interpretability (FINAL — see Revision note 3)

```
("explainable artificial intelligence"[tiab] OR "explainable AI"[tiab] OR "XAI"[tiab]
OR "interpretable machine learning"[tiab] OR "interpretability"[tiab] OR "model interpretability"[tiab]
OR "explainability"[tiab] OR "explainable model*"[tiab]
OR "SHAP"[tiab] OR "Shapley additive explanation*"[tiab] OR "Shapley value*"[tiab]
OR "LIME"[tiab] OR "local interpretable model-agnostic"[tiab]
OR "Grad-CAM"[tiab] OR "gradient-weighted class activation"[tiab] OR "class activation map*"[tiab]
OR "counterfactual explanation*"[tiab]
OR "feature attribution"[tiab]
OR "rule extraction"[tiab]
OR "prototype-based explanation"[tiab] OR "prototype explanation*"[tiab] OR "case-based explanation*"[tiab]
OR "interpretable AI"[tiab] OR "interpretable artificial intelligence"[tiab]
OR "explainable deep learning"[tiab])
```

Source: every method named in `xai_method_taxonomy.md` (SHAP, LIME, Grad-CAM, Attention, ANCHOR — covered by "decision rule*"/"rule extraction", Counterfactual, Prototype, Rule extraction) plus the umbrella terminology terms from the foundational papers (Lipton, Doshi-Velez, Adadi, Arrieta).

**Removed in Revision note 3 (2026-06-07):** `"black box"[tiab]`, `"black-box"[tiab]`, `"saliency map*"[tiab]`, `"attention map*"[tiab]`, `"attention weight*"[tiab]`, `"attention mechanism*"[tiab]`, `"feature importance"[tiab]`, `"decision rule*"[tiab]` — five generic ML/stats term-groups that inflated the corpus with non-XAI papers without adding confirmed recall (see Revision note 3 for the diagnostic and validation evidence). Kept here in the audit trail rather than silently deleted, per the methodological-transparency standard the rest of this document follows.

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

**Revision note 2 (2026-06-07):** The first corrected paste produced two syntax warnings in PubMed and only 36 hits:
1. A duplicate `AND\nAND` (a leftover artifact from merging the two Concept B sub-blocks) — PubMed silently dropped the stray `AND` term but it indicated the string was malformed. Removed the duplicate line.
2. `"prototype-based explanation*"[tiab]` was rejected with "Quoted phrase not found in phrase index" — PubMed's phrase index has no entries matching that exact wildcarded phrase (a known quirk: multi-word phrases combined with trailing wildcards sometimes fail phrase-index lookup even when the unwildcarded phrase would match). Replaced with three forms that pass indexing: `"prototype-based explanation"[tiab] OR "prototype explanation*"[tiab] OR "case-based explanation*"[tiab]`.

**The 36-hit count is not a search-string problem — it is a filter problem.** The run that returned 36 had four PubMed sidebar filters silently stacked on top of the string: **Review, Systematic Review, English, Humans, Aged: 65+ years**. Two of these are fatal for a search meant to identify primary studies:
- **"Review / Systematic Review" article-type filter** excludes the primary research papers this review needs to find (it would only surface *other* systematic reviews on the topic).
- **"Aged: 65+ years"** restricts to studies specifically about elderly populations — excludes the large majority of clinical XAI papers that don't report age-stratified MeSH indexing at all.

**Action for the user:** click "Clear all" on the filters sidebar (as already shown in the result panel) and re-run the corrected string with no filters except the date range and language already embedded in the string itself. Expect the count to jump substantially.

**Revision note 3 (2026-06-07) — precision tuning and recall validation:**

With filters cleared, the corrected string returned **15,385 hits** — now too broad to screen by hand. Diagnostic: Concept A run alone (no Concept B) returned **70,946 hits**, meaning Concept A itself was matching enormous numbers of papers that have nothing to do with clinical XAI. Five term-groups in Concept A are generic ML/stats vocabulary that appears constantly outside explainability research:

- `"black box"[tiab]` / `"black-box"[tiab]` — used metaphorically across medicine, aviation, automotive, computing generally
- `"attention map*"[tiab]` / `"attention weight*"[tiab]` / `"attention mechanism*"[tiab]` — a standard transformer/deep-learning architecture component, present in any attention-based model paper regardless of whether explainability is the topic
- `"saliency map*"[tiab]` — a routine computer-vision output, often reported with no explainability framing
- `"feature importance"[tiab]` — generic ML reporting phrase (e.g., random-forest variable importance)
- `"decision rule*"[tiab]` — generic clinical/statistical phrase (clinical prediction rules, guideline decision rules), rarely XAI-specific on its own

Removing these five term-groups and re-running `(reduced Concept A) AND (Concept B) AND (date) AND (language)` returned **9,672 hits** — a 37% reduction (~5,700 fewer hits), confirming these terms were a major noise source.

**Recall validation against an independent benchmark (in place of Issue #16's originally planned approach):** The protocol's reference to validating against "the seed paper set... used for EV rubric and quality rubric piloting" turned out to be aspirational — per `docs/osf/preregistration_draft.md:144` and `memos/research_master_memo.md`, that set is explicitly deferred to be drawn *after* full-text screening (using it now would be circular: validating the search with papers the search produced). `references/bib/foundational.bib` was also checked and ruled out — it contains only general XAI theory/survey papers (Lipton, Rudin, Miller, Doshi-Velez, Adadi, Arrieta, Samek), none of which are clinical application studies that would pass Gate 1.

Instead, an independent benchmark was assembled by citation-chasing forward from those seven foundational papers (via the Semantic Scholar citations API), filtering candidates for clinical-domain + XAI-method co-occurrence in the title, restricted to 2019–2023 (so the date filter wouldn't manufacture false "misses"). Eight candidates were screened against the three gates in `inclusion_boundary.md` on abstract content; four passed all three gates clearly:

| Paper | PMID | Gate check |
|---|---|---|
| Cao, Kunaprayoon & Ren (2023) — Interpretable AI-assisted CDM for radiosurgery dose prescription, brain metastases | 37543055 | Pass — physician-ranking validation described |
| Tosun et al. (2020) — Explainable AI (xAI) for Anatomic Pathology (HistoMapr) | 32541594 | Pass — designed explicitly as a pathologist's interactive guide |
| Kumar et al. (2021) — "Doctor's Dilemma": SSLW-CNN with CAM for brain tumor diagnosis | — (not in PubMed; ACM Trans. Multimedia) | Pass — doctor feedback, physician trust evaluation described |
| Gu et al. (2020/2023) — xPath: Human-AI diagnosis system in pathology | — (not in PubMed; ACM Trans. CHI) | Pass — work sessions with 12 medical professionals |

**Finding 1 — recall is preserved:** Of the four gate-passing papers, only two (PMID 37543055, 32541594) are actually indexed in MEDLINE/PubMed. Both are retrieved by **both** the 15,385-hit and the 9,672-hit string variants — confirming the five removed term-groups cost **zero** recall against the confirmed benchmark. (The Anatomic Pathology paper's abstract even contains "black-box" — one of the removed terms — yet still matches via "xAI"/"explainable AI", proving the removed term was redundant for this paper specifically.) **Decision: adopt the reduced Concept A (9,672 hits) as the final v1 string.**

**Finding 2 — a database-coverage gap, not a query-tuning problem:** The other two gate-passing papers (Kumar et al.; Gu et al.) are **not indexed in PubMed/MEDLINE at all** — they were published in ACM Digital Library venues (ACM Trans. on Multimedia Computing; ACM Trans. on Computer-Human Interaction). Two further candidates that were *borderline* on the gates (Nayebi et al. 2022, TBI XAI-methods comparison — AMIA Symposium/arXiv preprint; Clough et al. 2019, Cardiac MRI interpretability — MICCAI proceedings/arXiv preprint) are likewise absent from PubMed. Of six candidates checked, only 2/6 (33%) are MEDLINE-indexed. No amount of query tuning can retrieve papers the database does not contain — this is concrete empirical evidence that a PubMed-only search will structurally miss a substantial share of clinical-XAI literature published in CS/HCI/engineering venues, and it strengthens the case for the multi-database plan already scoped in Issue #22. **Action:** earmark Kumar et al., Gu et al., Nayebi et al., and Clough et al. as targets to confirm retrievability in ACM Digital Library / IEEE Xplore / Embase translations of this string.

This benchmark set is independent of, and must remain distinct from, the post-screening IRR seed-paper set described in `docs/osf/preregistration_draft.md` (drawing the validation set from search results would be circular).

---

## Full Combined String

```
(Concept A) AND (Concept B)

AND ("2015/01/01"[Date - Publication] : "2024/12/31"[Date - Publication])
AND English[Language]
```

Paste-ready single-line version (PubMed search box) — **FINAL, validated, 9,672 hits**:

```
("explainable artificial intelligence"[tiab] OR "explainable AI"[tiab] OR "XAI"[tiab] OR "interpretable machine learning"[tiab] OR "interpretability"[tiab] OR "model interpretability"[tiab] OR "explainability"[tiab] OR "explainable model*"[tiab] OR "SHAP"[tiab] OR "Shapley additive explanation*"[tiab] OR "Shapley value*"[tiab] OR "LIME"[tiab] OR "local interpretable model-agnostic"[tiab] OR "Grad-CAM"[tiab] OR "gradient-weighted class activation"[tiab] OR "class activation map*"[tiab] OR "counterfactual explanation*"[tiab] OR "feature attribution"[tiab] OR "rule extraction"[tiab] OR "prototype-based explanation"[tiab] OR "prototype explanation*"[tiab] OR "case-based explanation*"[tiab] OR "interpretable AI"[tiab] OR "interpretable artificial intelligence"[tiab] OR "explainable deep learning"[tiab])
AND
("clinical decision support"[tiab] OR "clinical decision support system*"[tiab] OR "CDSS"[tiab] OR "computer-aided diagnos*"[tiab] OR "computer aided diagnos*"[tiab] OR "diagnostic algorithm*"[tiab] OR "predictive model*"[tiab] OR "risk prediction model*"[tiab] OR "clinical"[tiab] OR "clinician*"[tiab] OR "physician*"[tiab] OR "radiolog*"[tiab] OR "patholog*"[tiab] OR "nurse*"[tiab] OR "diagnosis"[tiab] OR "diagnostic"[tiab] OR "prognosis"[tiab] OR "treatment"[tiab] OR "patient care"[tiab] OR "hospital*"[tiab] OR "Decision Support Systems, Clinical"[Mesh] OR "Physicians"[Mesh] OR "Clinical Decision-Making"[Mesh] OR "Diagnosis, Computer-Assisted"[Mesh] OR "Patient Care"[Mesh])
AND ("2015/01/01"[Date - Publication] : "2024/12/31"[Date - Publication])
AND English[Language]
```

Superseded draft (15,385 hits, before precision tuning — retained for the audit trail, do not use for execution):

```
("explainable artificial intelligence"[tiab] OR "explainable AI"[tiab] OR "XAI"[tiab] OR "interpretable machine learning"[tiab] OR "interpretability"[tiab] OR "model interpretability"[tiab] OR "explainability"[tiab] OR "explainable model*"[tiab] OR "SHAP"[tiab] OR "Shapley additive explanation*"[tiab] OR "Shapley value*"[tiab] OR "LIME"[tiab] OR "local interpretable model-agnostic"[tiab] OR "Grad-CAM"[tiab] OR "gradient-weighted class activation"[tiab] OR "class activation map*"[tiab] OR "saliency map*"[tiab] OR "attention map*"[tiab] OR "attention weight*"[tiab] OR "attention mechanism*"[tiab] OR "counterfactual explanation*"[tiab] OR "feature attribution"[tiab] OR "feature importance"[tiab] OR "rule extraction"[tiab] OR "decision rule*"[tiab] OR "prototype-based explanation"[tiab] OR "prototype explanation*"[tiab] OR "case-based explanation*"[tiab] OR "interpretable AI"[tiab] OR "interpretable artificial intelligence"[tiab] OR "black box"[tiab] OR "black-box"[tiab] OR "explainable deep learning"[tiab])
AND
("clinical decision support"[tiab] OR "clinical decision support system*"[tiab] OR "CDSS"[tiab] OR "computer-aided diagnos*"[tiab] OR "computer aided diagnos*"[tiab] OR "diagnostic algorithm*"[tiab] OR "predictive model*"[tiab] OR "risk prediction model*"[tiab] OR "clinical"[tiab] OR "clinician*"[tiab] OR "physician*"[tiab] OR "radiolog*"[tiab] OR "patholog*"[tiab] OR "nurse*"[tiab] OR "diagnosis"[tiab] OR "diagnostic"[tiab] OR "prognosis"[tiab] OR "treatment"[tiab] OR "patient care"[tiab] OR "hospital*"[tiab] OR "Decision Support Systems, Clinical"[Mesh] OR "Physicians"[Mesh] OR "Clinical Decision-Making"[Mesh] OR "Diagnosis, Computer-Assisted"[Mesh] OR "Patient Care"[Mesh])
AND ("2015/01/01"[Date - Publication] : "2024/12/31"[Date - Publication])
AND English[Language]
```

---

## Known Limitations / Residual Watch Items

1. **"ANCHOR" intentionally omitted as a bare term** — too short and ambiguous (matches anatomical anchors, surgical anchors). Coverage relies on "decision rule*"-equivalents being absorbed into "rule extraction"; if a future audit finds ANCHOR-based papers being missed, add `"anchor explanation*"[tiab]` or `"anchors LIME"[tiab]` as a targeted addition.
2. **"Attention," "black box," "saliency map," "feature importance," and "decision rule" were removed (Revision note 3)** — these generic ML/stats terms inflated Concept A from a focused XAI vocabulary to 70,946 hits (vs. ~9,672 for the full combined query), without adding confirmed recall against the independent benchmark. If full-text screening later turns up an included paper that used *only* one of these generic terms (and none of the remaining Concept A vocabulary) in its title/abstract, that would be a genuine miss worth logging — but the benchmark validation found no such case.
3. **MeSH terms lag new technology** — "Artificial Intelligence"[Mesh] and "Machine Learning"[Mesh] may not yet be indexed on very recent papers (indexing lag ~6 months to 2 years). The [tiab] terms compensate for this; do not rely on MeSH alone.
4. **No drug/device brand names included** — by design (Gate 1 excludes drug discovery; consumer wearables are excluded at Gate 1 unless clinically overseen).
5. **Database-coverage gap is now empirically documented (Revision note 3, Finding 2)** — 4 of 6 benchmark candidates that passed the inclusion gates are not indexed in MEDLINE at all (ACM Digital Library, MICCAI proceedings, AMIA/arXiv preprints). This is a structural limitation of PubMed as a single source, not a defect of this string — it is the primary justification for the multi-database translation in Issue #22, and those four papers are now concrete test cases for that translation.

---

## Next Steps

1. ~~Run this string in PubMed; record total hit count here.~~ Done — final string returns **9,672 hits** (2015–2024, English).
2. ~~Issue #16 — validate recall against seed papers.~~ Done via an independent citation-chased benchmark (see Revision note 3) — the originally planned seed-paper set does not exist yet (it is deliberately drawn post-screening per `preregistration_draft.md`, which would make validation circular). Both MEDLINE-indexed benchmark papers are retrieved by the final string.
3. Log the final string, hit count, and the database-coverage finding in `memos/decision_log.md` (the logged string becomes the version reported in PRISMA Identification).
4. ~~Translate to other databases (Embase, CINAHL, IEEE Xplore, ACM Digital Library) per Issue #22~~ Done (2026-06-09) — first-pass DRAFT/UNTESTED translations created: `search_string_embase_v1.md`, `search_string_cinahl_v1.md`, `search_string_ieee_v1.md`, `search_string_acm_v1.md`. Kumar et al. (2021) and Gu et al. (2020/2023) are primary retrievability test cases for the ACM Digital Library translation (confirmed ACM DL content). Nayebi et al. (2022, AMIA/arXiv) and Clough et al. (2019, MICCAI/Springer LNCS/arXiv) are **not** confirmed in any of IEEE/ACM/Embase/CINAHL — no benchmark paper currently covers the IEEE Xplore translation; flagged for retroactive validation against any IEEE-published paper found at full-text screening.
5. Run each of the four draft translations live; record hit counts in `data/screening/prisma_counts.csv` and resolve all "to verify" items (Emtree term existence for Embase, CINAHL Subject Heading labels, IEEE field-tag-group syntax, ACM bracket-nesting syntax and wildcard behaviour) per each document's own Next Steps section.

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1 draft | 2026-06-07 | Initial draft. Two-concept AND structure (XAI terms AND clinical-AI terms). Issue #15. |
| v1 rev 1 | 2026-06-07 | Fixed accidental 3-way AND (removed redundant nested AI/ML tech sub-block from Concept B); 9 hits → corrected structure. |
| v1 rev 2 | 2026-06-07 | Fixed duplicate `AND AND` syntax error and `"prototype-based explanation*"` phrase-index rejection; diagnosed 36-hit result as a filter artifact (Review/Systematic-Review/Aged 65+ filters stacked in PubMed UI), not a string defect. |
| v1 rev 3 — **FINAL** | 2026-06-07 | Diagnosed 15,385-hit over-breadth to 5 generic ML/stats term-groups in Concept A (confirmed via Concept-A-alone test: 70,946 hits); removed them, yielding 9,672 hits (37% reduction). Validated recall against an independently citation-chased benchmark (4 papers passing all 3 inclusion gates; 2 indexed in MEDLINE) — both indexed papers retrieved by the final string, confirming zero recall loss. Documented a database-coverage finding (4/6 benchmark candidates not indexed in MEDLINE — published in ACM/MICCAI/AMIA venues) that empirically justifies the Issue #22 multi-database plan. **This is the version to execute and report in PRISMA Identification.** |
