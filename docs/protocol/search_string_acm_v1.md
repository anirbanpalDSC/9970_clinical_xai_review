# ACM Digital Library Search String v1 — Clinical XAI Systematic Review (9970)

**Issue:** #22
**Status:** DRAFT / UNTESTED — translated from the validated PubMed v1 rev 3 string (`search_string_pubmed_v1.md`, 9,672 hits). Not yet run against live ACM Digital Library. Hit counts, bracket-nesting custom-query syntax, and wildcard behaviour all require live verification.
**Database:** ACM Digital Library (Advanced Search → "Edit Query" / Full Query Syntax)
**Date range filter (target):** 2015–2024
**Language filter (target):** English (no separate language field — see Known Limitations)

---

## Design Rationale

This is a field-syntax translation of the finalized PubMed v1 rev 3 string (see `search_string_pubmed_v1.md` for the full diagnostic history: 9 → 36 → 15,385 → 9,672 hits). The two-concept AND structure is preserved:

- **Concept A — XAI / Interpretability**
- **Concept B — Clinical / Medical Context**

As with IEEE Xplore, **the 5 MeSH terms in Concept B are dropped entirely** — ACM DL's controlled vocabulary (the ACM Computing Classification System, CCS) is a CS-topic taxonomy with no clinical/medical concepts (no equivalent of "Patient Care" or "Clinical Decision-Making"). Concept B is free-text-only here.

**This is the most important database of the four for recall validation.** Two of the four non-MEDLINE benchmark papers identified during PubMed validation (`search_string_pubmed_v1.md` Revision note 3, Finding 2) are **confirmed ACM Digital Library content**:

| Paper | Venue | Gate check |
|---|---|---|
| Kumar et al. (2021) — "Doctor's Dilemma": SSLW-CNN with CAM for brain tumor diagnosis | ACM Trans. on Multimedia Computing, Communications, and Applications | Pass — doctor feedback, physician trust evaluation described |
| Gu et al. (2020/2023) — xPath: Human-AI diagnosis system in pathology | ACM Trans. on Computer-Human Interaction | Pass — work sessions with 12 medical professionals |

**These two papers are the primary retrievability test cases for this string.** Before trusting any hit count from this database:
1. Search for each paper directly by title to confirm it exists in ACM DL (sanity check).
2. Confirm both are retrieved by the Full Combined String below.
3. If either is missed, diagnose which concept's term list failed to match (Kumar et al.'s title contains "CAM" → Concept A's `"class activation map*"` should match if title indexing covers acronym expansion — but "CAM" as a bare 3-letter acronym is not in the Concept A list as a standalone term, only as part of "class activation map*" and "Grad-CAM"; this is a known gap to watch for).

---

## Concept A — XAI / Interpretability (DRAFT, free-text only)

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

**Translation notes:**
- Double quotes preserved for exact-phrase matching.
- **Truncation symbol `*` is UNVERIFIED for ACM DL.** Web documentation is contradictory: some sources describe `*` as a multi-character wildcard (the conventional meaning, same as PubMed/Embase/CINAHL/IEEE), others describe ACM DL wildcards as single-character substitution only. **Test a single wildcarded term first** (e.g., search `Title:(explainable model*)` via "Search Within"/Title field and compare against `Title:("explainable models" OR "explainable model")`). If `*` does not behave as multi-character truncation:
  - Replace each wildcarded term with explicit singular/plural (or other) variants as separate OR'd phrases. The wildcarded terms here are: `"explainable model*"`, `"Shapley additive explanation*"`, `"Shapley value*"`, `"class activation map*"`, `"counterfactual explanation*"`, `"prototype explanation*"`, `"case-based explanation*"` (Concept A) and `"clinical decision support system*"`, `"computer-aided diagnos*"`, `"computer aided diagnos*"`, `"diagnostic algorithm*"`, `"predictive model*"`, `"risk prediction model*"`, `"clinician*"`, `"radiolog*"`, `"patholog*"`, `"nurse*"`, `"hospital*"` (Concept B).
- No CCS controlled-vocabulary additions — ACM's classification taxonomy has no XAI-specific concepts beyond very broad ones (e.g., "Computing methodologies → Machine learning"), which would risk the same over-broadening diagnosed in PubMed v1 rev 3.

---

## Concept B — Clinical / Medical Context (DRAFT, free-text only — MeSH terms dropped)

```
"clinical decision support" OR "clinical decision support system*" OR CDSS
OR "computer-aided diagnos*" OR "computer aided diagnos*"
OR "diagnostic algorithm*" OR "predictive model*" OR "risk prediction model*"
OR clinical OR "clinician*" OR "physician*" OR "radiolog*"
OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic
OR prognosis OR treatment OR "patient care" OR "hospital*"
```

**Translation notes:**
- The 5 MeSH terms are dropped — same rationale as the IEEE Xplore translation (no clinical controlled vocabulary in ACM DL's CCS taxonomy).
- ACM DL's corpus is overwhelmingly CS/HCI/engineering — the broad single-word terms (`clinical`, `diagnosis`, `treatment`, `prognosis`, `hospital*`) are expected to do most of the discriminating work here, similar to IEEE. Given ACM DL's much smaller absolute size compared to PubMed/Embase, an over-broad Concept B is less likely to produce an unmanageable count than it would in IEEE — but still verify.

---

## Full Combined String (DRAFT — build via Advanced Search UI, then inspect/edit via "View Query Syntax")

**Recommended workflow** (per ACM DL's interface): use the Advanced Search "Search Within" builder to construct one row per field (Title, Abstract, Keyword) for each concept, combine with AND/OR, then click "View Query Syntax" to see the generated bracket-nested custom query — and use the "Edit Query" box to paste the full string below directly, adjusting bracket nesting to match what the UI generates if it differs.

```
[[Title: (Concept A)] OR [Abstract: (Concept A)] OR [Keyword: (Concept A)]]
AND
[[Title: (Concept B)] OR [Abstract: (Concept B)] OR [Keyword: (Concept B)]]
```

```
[[Title: ("explainable artificial intelligence" OR "explainable AI" OR XAI OR "interpretable machine learning" OR interpretability OR "model interpretability" OR explainability OR "explainable model*" OR SHAP OR "Shapley additive explanation*" OR "Shapley value*" OR LIME OR "local interpretable model-agnostic" OR "Grad-CAM" OR "gradient-weighted class activation" OR "class activation map*" OR "counterfactual explanation*" OR "feature attribution" OR "rule extraction" OR "prototype-based explanation" OR "prototype explanation*" OR "case-based explanation*" OR "interpretable AI" OR "interpretable artificial intelligence" OR "explainable deep learning")]
OR [Abstract: ("explainable artificial intelligence" OR "explainable AI" OR XAI OR "interpretable machine learning" OR interpretability OR "model interpretability" OR explainability OR "explainable model*" OR SHAP OR "Shapley additive explanation*" OR "Shapley value*" OR LIME OR "local interpretable model-agnostic" OR "Grad-CAM" OR "gradient-weighted class activation" OR "class activation map*" OR "counterfactual explanation*" OR "feature attribution" OR "rule extraction" OR "prototype-based explanation" OR "prototype explanation*" OR "case-based explanation*" OR "interpretable AI" OR "interpretable artificial intelligence" OR "explainable deep learning")]
OR [Keyword: ("explainable artificial intelligence" OR "explainable AI" OR XAI OR "interpretable machine learning" OR interpretability OR "model interpretability" OR explainability OR "explainable model*" OR SHAP OR "Shapley additive explanation*" OR "Shapley value*" OR LIME OR "local interpretable model-agnostic" OR "Grad-CAM" OR "gradient-weighted class activation" OR "class activation map*" OR "counterfactual explanation*" OR "feature attribution" OR "rule extraction" OR "prototype-based explanation" OR "prototype explanation*" OR "case-based explanation*" OR "interpretable AI" OR "interpretable artificial intelligence" OR "explainable deep learning")]]
AND
[[Title: ("clinical decision support" OR "clinical decision support system*" OR CDSS OR "computer-aided diagnos*" OR "computer aided diagnos*" OR "diagnostic algorithm*" OR "predictive model*" OR "risk prediction model*" OR clinical OR "clinician*" OR "physician*" OR "radiolog*" OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic OR prognosis OR treatment OR "patient care" OR "hospital*")]
OR [Abstract: ("clinical decision support" OR "clinical decision support system*" OR CDSS OR "computer-aided diagnos*" OR "computer aided diagnos*" OR "diagnostic algorithm*" OR "predictive model*" OR "risk prediction model*" OR clinical OR "clinician*" OR "physician*" OR "radiolog*" OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic OR prognosis OR treatment OR "patient care" OR "hospital*")]
OR [Keyword: ("clinical decision support" OR "clinical decision support system*" OR CDSS OR "computer-aided diagnos*" OR "computer aided diagnos*" OR "diagnostic algorithm*" OR "predictive model*" OR "risk prediction model*" OR clinical OR "clinician*" OR "physician*" OR "radiolog*" OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic OR prognosis OR treatment OR "patient care" OR "hospital*")]]
```

**Date filter:** apply 2015–2024 via the **"Publication Date"** facet/filter in the Advanced Search results page (custom range option), not embedded in the query string. **Same filter-stacking caution as the PubMed 36-hit incident**: after applying the date range, check the full facet panel (Content Type, Publisher, etc.) for any other filters that may have carried over from a previous search session, and clear them unless deliberately chosen.

---

## Known Limitations / Things to Verify Live

1. **Bracket-nesting custom query syntax is unverified** — the `[[Field: (...)] OR [Field: (...)]]` structure shown above is based on documentation references to ACM DL's "Full Query Syntax"/"Edit Query" feature, but the exact nesting/parenthesization rules need confirmation. **Recommended approach: build the search via the Advanced Search UI form first** (one "Search Within" row per field per concept), then click "View Query Syntax" to see the system-generated equivalent — use that as the template and substitute in the full term lists.
2. **Wildcard (`*`) behaviour is unverified** — see Concept A translation notes above for the fallback (manual variant expansion) if `*` doesn't truncate as expected.
3. **No language filter** — ACM DL has no dedicated language field; the corpus is predominantly English. Non-English results, if any, would need handling at the screening stage.
4. **No proximity operators** — PubMed's string doesn't use proximity operators either, so this isn't a translation loss, but note it for any future refinements (e.g., if precision tuning later wants "explainable NEAR/3 model").
5. **`Keyword` field scope** — ACM DL's "Keyword" field may correspond to author-supplied keywords, CCS concepts, or both depending on the platform version; verify what it actually searches. If it behaves unexpectedly (e.g., matching only controlled CCS terms, none of which are in our free-text lists), drop the `[Keyword: ...]` clauses and use `[Title: ...] OR [Abstract: ...]` only (a 2-field, not 3-field, OR — directly analogous to PubMed's `[tiab]`).
6. **5 MeSH terms dropped** — same situation and rationale as IEEE Xplore.

---

## Next Steps

1. Sanity-check: search ACM DL by title for "Doctor's Dilemma" (Kumar et al. 2021) and "xPath" (Gu et al.) to confirm both are indexed and locate their Title/Abstract/Keyword field content.
2. Build the Concept A + Concept B search via the Advanced Search UI form (one row per field per concept), then use "View Query Syntax" to confirm/correct the bracket-nesting template above.
3. Test wildcard behaviour on one term (e.g., `"explainable model*"`); apply the manual-variant fallback across both concept blocks if needed.
4. Run the Full Combined String; confirm both Kumar et al. and Gu et al. appear in the result set. If either is missing, diagnose per the retrievability test-case note above.
5. Apply the Publication Date filter (2015–2024), checking for stacked facets per the caution above.
6. Record the final hit count here and in `data/screening/prisma_counts.csv` (row "Records from database: ACM Digital Library").
7. Once stable, log the final string, hit count, and the Kumar/Gu retrievability result in `memos/decision_log.md`.

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1 draft (UNTESTED) | 2026-06-09 | Initial translation from PubMed v1 rev 3 (9,672 hits). 5 MeSH terms dropped (no ACM CCS equivalent); bracket-nested `[Field: (...)]` custom query syntax proposed but unverified; Kumar et al. (2021) and Gu et al. (2020/2023) identified as primary retrievability test cases (both confirmed ACM DL content). Not yet run live. |
