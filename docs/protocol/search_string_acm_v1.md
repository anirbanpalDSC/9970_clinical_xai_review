# ACM Digital Library Search String v1 (rev 2 — EM-narrowed) — Clinical XAI Scoping Review (9970)

**Issue:** #22
**Status:** DRAFT / UNTESTED — v2, EM-narrowed (A+B+C). Translated from `search_string_pubmed_v1.md` v2 FINAL (A+B+C: 213 hits 2015-2024 / 497 hits 2015-2026/06/10, live-verified via E-utilities). Supersedes the original v1 cross-domain draft (A+B only, translated from the now-superseded 9,672-hit PubMed cross-domain string). Not yet run against live ACM Digital Library.
**Database:** ACM Digital Library (Advanced Search → "Edit Query" / Full Query Syntax)
**Date range filter (target):** 2015/01/01 through search-execution date (rolling "to present" window — see `memos/decision_log.md`, 2026-06-10. PubMed reference snapshot taken 2026-06-10: A+B+C = 497 hits)
**Language filter (target):** English (no separate language field — see Known Limitations)

---

## Design Rationale

This is a field-syntax translation of the EM-narrowed PubMed v2 FINAL string (`search_string_pubmed_v1.md`). The three-concept AND structure is preserved:

- **Concept A — XAI / Interpretability** (unchanged from the v1 cross-domain translation)
- **Concept B — Clinical / Medical Context** (unchanged from the v1 cross-domain translation; 5 MeSH terms dropped, free-text only — see v1 history)
- **Concept C — Emergency Medicine / ED / Triage / Acuity / Disposition** (NEW for the 2026-06-10 EM pivot; the 2 MeSH-equivalent terms in the PubMed Concept C block are dropped, same rationale as Concept B's dropped MeSH terms — ACM CCS has no clinical/medical concepts)

**This remains the most important database of the four for recall validation** — Kumar et al. (2021) and Gu et al. (2020/2023) (see v1 Design Rationale for full citations and gate-check notes) are confirmed ACM Digital Library content and the primary retrievability test cases. **However, neither paper has been checked against the v2 EM inclusion boundary (`docs/protocol/inclusion_boundary.md` v2)** — both are imaging/pathology diagnosis papers, not ED-encounter (intake/triage/disposition) papers, so they may legitimately fail Concept C and no longer be expected to appear in the A+B+C result set. Treat their retrieval (or non-retrieval) as diagnostic of *which concept* is filtering them out, not as a pass/fail criterion for the v2 string itself (see Next Steps).

---

## Concept A — XAI / Interpretability (unchanged from v1, free-text only)

```
"explainable artificial intelligence" OR "explainable AI" OR XAI
OR "interpretable machine learning" OR interpretability OR "model interpretability"
OR explainability OR "explainable model*"
OR SHAP OR "Shapley additive explanation*" OR "Shapley value*"
OR LIME OR "local interpretable model-agnostic"
OR "Grad-CAM" OR "gradient-weighted class activation" OR "class activation map*"
OR "counterfactual explanation*"
OR "feature attribution"
OR "rule extraction"
OR "prototype-based explanation" OR "prototype explanation*" OR "case-based explanation*"
OR "interpretable AI" OR "interpretable artificial intelligence"
OR "explainable deep learning"
```

Truncation (`*`) verification status unchanged from v1 — see v1 Concept A translation notes for the fallback (manual variant expansion) if `*` doesn't behave as multi-character truncation.

---

## Concept B — Clinical / Medical Context (unchanged from v1, free-text only — MeSH terms dropped)

```
"clinical decision support" OR "clinical decision support system*" OR CDSS
OR "computer-aided diagnos*" OR "computer aided diagnos*"
OR "diagnostic algorithm*" OR "predictive model*" OR "risk prediction model*"
OR clinical OR "clinician*" OR "physician*" OR "radiolog*"
OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic
OR prognosis OR treatment OR "patient care" OR "hospital*"
```

---

## Concept C — Emergency Medicine / ED / Triage / Acuity / Disposition (NEW, 2026-06-10, free-text only)

```
"emergency department" OR "emergency room" OR "emergency medicine"
OR "emergency severity index" OR ESI OR Triage
OR "acuity scor*" OR "acuity assessment" OR "acuity level*" OR "acuity classification"
OR "disposition decision*" OR "ED disposition" OR "discharge disposition"
OR "patient intake"
```

**Translation notes:**
- The 2 MeSH-equivalent terms from the PubMed Concept C block are dropped — same rationale as Concept B (no ACM CCS clinical vocabulary). `Triage` as a free-text term covers most of the dropped "Triage"[Mesh] concept.
- Wildcarded terms in this block (`"acuity scor*"`, `"acuity level*"`, `"disposition decision*"`) are subject to the same `*`-truncation verification as Concept A/B — add to the fallback variant-expansion list if `*` does not truncate as expected: `"acuity score"`/`"acuity scores"`/`"acuity scoring"`, `"acuity level"`/`"acuity levels"`, `"disposition decision"`/`"disposition decisions"`.
- **ACM DL's corpus is overwhelmingly CS/HCI/engineering** — Concept C should sharply narrow the result set relative to the cross-domain A+B string, similar to the PubMed 9,672 -> 213-497 narrowing. If Concept C contributes few or no additional hits beyond A+B, this may indicate ACM DL simply has very little ED-specific clinical XAI work — a plausible and informative null result, not necessarily a translation error.

---

## Full Combined String (DRAFT — build via Advanced Search UI, then inspect/edit via "View Query Syntax")

```
[[Title: (Concept A)] OR [Abstract: (Concept A)] OR [Keyword: (Concept A)]]
AND
[[Title: (Concept B)] OR [Abstract: (Concept B)] OR [Keyword: (Concept B)]]
AND
[[Title: (Concept C)] OR [Abstract: (Concept C)] OR [Keyword: (Concept C)]]
```

```
[[Title: ("explainable artificial intelligence" OR "explainable AI" OR XAI OR "interpretable machine learning" OR interpretability OR "model interpretability" OR explainability OR "explainable model*" OR SHAP OR "Shapley additive explanation*" OR "Shapley value*" OR LIME OR "local interpretable model-agnostic" OR "Grad-CAM" OR "gradient-weighted class activation" OR "class activation map*" OR "counterfactual explanation*" OR "feature attribution" OR "rule extraction" OR "prototype-based explanation" OR "prototype explanation*" OR "case-based explanation*" OR "interpretable AI" OR "interpretable artificial intelligence" OR "explainable deep learning")]
OR [Abstract: ("explainable artificial intelligence" OR "explainable AI" OR XAI OR "interpretable machine learning" OR interpretability OR "model interpretability" OR explainability OR "explainable model*" OR SHAP OR "Shapley additive explanation*" OR "Shapley value*" OR LIME OR "local interpretable model-agnostic" OR "Grad-CAM" OR "gradient-weighted class activation" OR "class activation map*" OR "counterfactual explanation*" OR "feature attribution" OR "rule extraction" OR "prototype-based explanation" OR "prototype explanation*" OR "case-based explanation*" OR "interpretable AI" OR "interpretable artificial intelligence" OR "explainable deep learning")]
OR [Keyword: ("explainable artificial intelligence" OR "explainable AI" OR XAI OR "interpretable machine learning" OR interpretability OR "model interpretability" OR explainability OR "explainable model*" OR SHAP OR "Shapley additive explanation*" OR "Shapley value*" OR LIME OR "local interpretable model-agnostic" OR "Grad-CAM" OR "gradient-weighted class activation" OR "class activation map*" OR "counterfactual explanation*" OR "feature attribution" OR "rule extraction" OR "prototype-based explanation" OR "prototype explanation*" OR "case-based explanation*" OR "interpretable AI" OR "interpretable artificial intelligence" OR "explainable deep learning")]]
AND
[[Title: ("clinical decision support" OR "clinical decision support system*" OR CDSS OR "computer-aided diagnos*" OR "computer aided diagnos*" OR "diagnostic algorithm*" OR "predictive model*" OR "risk prediction model*" OR clinical OR "clinician*" OR "physician*" OR "radiolog*" OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic OR prognosis OR treatment OR "patient care" OR "hospital*")]
OR [Abstract: ("clinical decision support" OR "clinical decision support system*" OR CDSS OR "computer-aided diagnos*" OR "computer aided diagnos*" OR "diagnostic algorithm*" OR "predictive model*" OR "risk prediction model*" OR clinical OR "clinician*" OR "physician*" OR "radiolog*" OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic OR prognosis OR treatment OR "patient care" OR "hospital*")]
OR [Keyword: ("clinical decision support" OR "clinical decision support system*" OR CDSS OR "computer-aided diagnos*" OR "computer aided diagnos*" OR "diagnostic algorithm*" OR "predictive model*" OR "risk prediction model*" OR clinical OR "clinician*" OR "physician*" OR "radiolog*" OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic OR prognosis OR treatment OR "patient care" OR "hospital*")]]
AND
[[Title: ("emergency department" OR "emergency room" OR "emergency medicine" OR "emergency severity index" OR ESI OR Triage OR "acuity scor*" OR "acuity assessment" OR "acuity level*" OR "acuity classification" OR "disposition decision*" OR "ED disposition" OR "discharge disposition" OR "patient intake")]
OR [Abstract: ("emergency department" OR "emergency room" OR "emergency medicine" OR "emergency severity index" OR ESI OR Triage OR "acuity scor*" OR "acuity assessment" OR "acuity level*" OR "acuity classification" OR "disposition decision*" OR "ED disposition" OR "discharge disposition" OR "patient intake")]
OR [Keyword: ("emergency department" OR "emergency room" OR "emergency medicine" OR "emergency severity index" OR ESI OR Triage OR "acuity scor*" OR "acuity assessment" OR "acuity level*" OR "acuity classification" OR "disposition decision*" OR "ED disposition" OR "discharge disposition" OR "patient intake")]]
```

**Date filter:** apply 2015 through the actual search-execution date via the **"Publication Date"** facet/filter (custom range option) — rolling "to present" per `memos/decision_log.md` (2026-06-10), not a fixed 2015-2024 range. Same filter-stacking caution as v1: check the full facet panel for any other filters carried over from a previous session.

---

## Known Limitations / Things to Verify Live

1. **Bracket-nesting custom query syntax is unverified** — unchanged from v1, now with a third `[Field: (...)]` triplet for Concept C.
2. **Wildcard (`*`) behaviour is unverified** — unchanged from v1; Concept C adds 3 more wildcarded terms (see Concept C translation notes).
3. **No language filter** — unchanged from v1.
4. **No proximity operators** — unchanged from v1.
5. **`Keyword` field scope** — unchanged from v1.
6. **Both MeSH-equivalent terms dropped from Concept C** — same situation and rationale as Concept B's 5 dropped MeSH terms.
7. **Retrievability test cases (Kumar et al., Gu et al.) may legitimately fail Concept C** — see Design Rationale; do not treat their absence from the A+B+C result set as a translation error without first checking whether they pass the v2 EM inclusion boundary (`docs/protocol/inclusion_boundary.md` v2) at all.

---

## Next Steps

1. Sanity-check: search ACM DL by title for "Doctor's Dilemma" (Kumar et al. 2021) and "xPath" (Gu et al.) to confirm both are indexed, as in v1.
2. Build the Concept A + B + C search via the Advanced Search UI form, then use "View Query Syntax" to confirm/correct the bracket-nesting template above.
3. Test wildcard behaviour on one term from each concept; apply the manual-variant fallback across all three blocks if needed.
4. Run the Full Combined String (A+B+C); compare the result count against the PubMed A+B+C reference (213 @ 2015-2024 / 497 @ 2015-2026/06/10). Check whether Kumar et al. and/or Gu et al. appear — if either is missing, first check against `docs/protocol/inclusion_boundary.md` v2 (Design Rationale) before treating it as a translation gap.
5. Apply the Publication Date filter (2015 through the actual search-execution date), checking for stacked facets per the caution above.
6. Record the final hit count here and in `data/screening/prisma_counts.csv` (row "Records from database: ACM Digital Library").
7. Once stable, log the final string, hit count, and the Kumar/Gu retrievability result in `memos/decision_log.md`.

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1 draft (UNTESTED) | 2026-06-09 | Initial translation from PubMed cross-domain v1 rev 3 (9,672 hits, A+B only). 5 MeSH terms dropped (no ACM CCS equivalent); bracket-nested `[Field: (...)]` custom query syntax proposed but unverified; Kumar et al. (2021) and Gu et al. (2020/2023) identified as primary retrievability test cases. Not yet run live. |
| v2 draft (UNTESTED, EM-narrowed) | 2026-06-10 | EM pivot: Concept C (ED/triage/ESI/acuity/disposition, free text only) added; restructured to A+B+C; date range extended from fixed 2015-2024 to rolling "2015 through search-execution date" per `memos/decision_log.md` (2026-06-10). Translated from PubMed v2 FINAL (A+B+C: 213 hits @ 2015-2024 / 497 hits @ 2015-2026/06/10). Noted that Kumar et al./Gu et al. retrievability test cases may legitimately fail Concept C under the v2 EM inclusion boundary. Not yet run live. |
