# CINAHL Search String v1 — Clinical XAI Systematic Review (9970)

**Issue:** #22
**Status:** DRAFT / UNTESTED — translated from the validated PubMed v1 rev 3 string (`search_string_pubmed_v1.md`, 9,672 hits). Not yet run against live CINAHL. Hit counts, CINAHL Subject Heading existence, and date/language limiter syntax all require live verification.
**Database:** CINAHL (CINAHL Complete / CINAHL Plus, via EBSCOhost)
**Date range filter (target):** 2015–2024
**Language filter (target):** English

---

## Design Rationale

This is a field-syntax translation of the finalized PubMed v1 rev 3 string (see `search_string_pubmed_v1.md` for the full diagnostic history: 9 → 36 → 15,385 → 9,672 hits). The same two-concept AND structure is preserved:

- **Concept A — XAI / Interpretability**
- **Concept B — Clinical / Medical Context**

EBSCOhost has no single field code equivalent to PubMed's `[tiab]` (title+abstract combined). The standard systematic-review convention is to OR together two field-restricted blocks:

```
( TI ( ...terms... ) ) OR ( AB ( ...terms... ) )
```

This is functionally equivalent to PubMed's `[tiab]` and is used for both Concept A and Concept B below.

**Recall validation status:** Both MEDLINE-indexed benchmark papers from the PubMed validation (PMID 37543055 — Cao, Kunaprayoon & Ren 2023; PMID 32541594 — Tosun et al. 2020) are health-sciences journal articles and are plausible CINAHL candidates, but **CINAHL's coverage is nursing/allied-health focused and does not guarantee inclusion of every MEDLINE-indexed biomedical-engineering/AI paper** — unlike Embase, CINAHL is not a MEDLINE superset. Treat these two PMIDs as "if found, good confirmation" rather than "must be found" test cases for this database. Do not treat their absence from CINAHL as a string defect.

---

## Concept A — XAI / Interpretability (DRAFT)

```
( TI ( "explainable artificial intelligence" OR "explainable AI" OR XAI
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
OR "explainable deep learning" ) )
OR
( AB ( "explainable artificial intelligence" OR "explainable AI" OR XAI
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
OR "explainable deep learning" ) )
```

**Translation notes:**
- `[tiab]` → `TI (...) OR AB (...)` (see Design Rationale).
- Truncation symbol `*` is unchanged — CINAHL/EBSCOhost uses the same `*` wildcard as PubMed for "zero or more characters" at the end of a term.
- Double quotes preserved — EBSCOhost uses `"..."` for exact-phrase matching, same as PubMed.
- No Emtree-style controlled-vocabulary additions are proposed for Concept A (CINAHL Subject Headings are health-care/nursing-oriented and unlikely to have dedicated headings for ML/XAI methods like SHAP, LIME, or Grad-CAM — these remain free-text-only concepts in this database, same as PubMed).
- **Spelling-variant wildcard not yet used:** EBSCOhost also supports `#` for an optional embedded character (e.g., `p#ediatric` matches both "pediatric" and "paediatric") and `?` for exactly one character. None of the current Concept A terms have known British/American spelling variants, so neither is used here — flag during live testing if any term (e.g., a "-ize"/"-ise" variant) needs this.

---

## Concept B — Clinical / Medical Context (DRAFT)

```
( TI ( "clinical decision support" OR "clinical decision support system*" OR CDSS
OR "computer-aided diagnos*" OR "computer aided diagnos*"
OR "diagnostic algorithm*" OR "predictive model*" OR "risk prediction model*"
OR clinical OR "clinician*" OR "physician*" OR "radiolog*"
OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic
OR prognosis OR treatment OR "patient care" OR "hospital*" ) )
OR
( AB ( "clinical decision support" OR "clinical decision support system*" OR CDSS
OR "computer-aided diagnos*" OR "computer aided diagnos*"
OR "diagnostic algorithm*" OR "predictive model*" OR "risk prediction model*"
OR clinical OR "clinician*" OR "physician*" OR "radiolog*"
OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic
OR prognosis OR treatment OR "patient care" OR "hospital*" ) )
OR
( (MH "Decision Support Systems, Clinical+") OR (MH "Physicians+")
OR (MH "Decision Making, Clinical+") OR (MH "Diagnosis, Computer Assisted+")
OR (MH "Patient Care+") )
```

**MeSH → CINAHL Subject Heading mapping table (all 5 candidates below MUST be verified via the CINAHL Subject Headings browser before this string is run for the record — CINAHL Headings are partly aligned with MeSH but frequently differ in word order, hyphenation, or pluralization):**

| PubMed MeSH term | CINAHL Heading candidate (UNVERIFIED) | Notes |
|---|---|---|
| "Decision Support Systems, Clinical"[Mesh] | `(MH "Decision Support Systems, Clinical+")` | CINAHL often shares this exact heading with MeSH — reasonably likely to match as-is |
| "Physicians"[Mesh] | `(MH "Physicians+")` | Verify exact label — CINAHL may use "Physicians" or a more specific heading set |
| "Clinical Decision-Making"[Mesh] | `(MH "Decision Making, Clinical+")` | **Word order differs from MeSH** ("Decision Making, Clinical" vs. "Clinical Decision-Making") — this is the most likely candidate to need correction; confirm via the heading browser |
| "Diagnosis, Computer-Assisted"[Mesh] | `(MH "Diagnosis, Computer Assisted+")` | Verify whether CINAHL retains the comma/hyphen from the MeSH label |
| "Patient Care"[Mesh] | `(MH "Patient Care+")` | Likely a direct match |

**The `+` suffix inside the quoted heading denotes "explode" (include narrower terms)** — the EBSCOhost equivalent of PubMed's MeSH explosion (which is the default behavior for `[Mesh]` terms). If a heading doesn't exist as written, the EBSCOhost interface will typically suggest the nearest valid heading when you search the Subject Headings browser directly — use that suggestion rather than guessing further variants.

---

## Full Combined String (DRAFT — paste into CINAHL advanced search "Find all my search terms" box for first live test)

```
(Concept A) AND (Concept B)
```

```
( ( TI ( "explainable artificial intelligence" OR "explainable AI" OR XAI OR "interpretable machine learning" OR interpretability OR "model interpretability" OR explainability OR "explainable model*" OR SHAP OR "Shapley additive explanation*" OR "Shapley value*" OR LIME OR "local interpretable model-agnostic" OR "Grad-CAM" OR "gradient-weighted class activation" OR "class activation map*" OR "counterfactual explanation*" OR "feature attribution" OR "rule extraction" OR "prototype-based explanation" OR "prototype explanation*" OR "case-based explanation*" OR "interpretable AI" OR "interpretable artificial intelligence" OR "explainable deep learning" ) ) OR ( AB ( "explainable artificial intelligence" OR "explainable AI" OR XAI OR "interpretable machine learning" OR interpretability OR "model interpretability" OR explainability OR "explainable model*" OR SHAP OR "Shapley additive explanation*" OR "Shapley value*" OR LIME OR "local interpretable model-agnostic" OR "Grad-CAM" OR "gradient-weighted class activation" OR "class activation map*" OR "counterfactual explanation*" OR "feature attribution" OR "rule extraction" OR "prototype-based explanation" OR "prototype explanation*" OR "case-based explanation*" OR "interpretable AI" OR "interpretable artificial intelligence" OR "explainable deep learning" ) ) )
AND
( ( TI ( "clinical decision support" OR "clinical decision support system*" OR CDSS OR "computer-aided diagnos*" OR "computer aided diagnos*" OR "diagnostic algorithm*" OR "predictive model*" OR "risk prediction model*" OR clinical OR "clinician*" OR "physician*" OR "radiolog*" OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic OR prognosis OR treatment OR "patient care" OR "hospital*" ) ) OR ( AB ( "clinical decision support" OR "clinical decision support system*" OR CDSS OR "computer-aided diagnos*" OR "computer aided diagnos*" OR "diagnostic algorithm*" OR "predictive model*" OR "risk prediction model*" OR clinical OR "clinician*" OR "physician*" OR "radiolog*" OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic OR prognosis OR treatment OR "patient care" OR "hospital*" ) ) OR ( (MH "Decision Support Systems, Clinical+") OR (MH "Physicians+") OR (MH "Decision Making, Clinical+") OR (MH "Diagnosis, Computer Assisted+") OR (MH "Patient Care+") ) )
```

**Date and language: apply via Limiters panel, not inline syntax.** Unlike PubMed (`[Date - Publication]`, `[Language]`) and Embase (`/py`, `/lim`), EBSCOhost's standard advanced-search interface applies date range and language as **Limiters checkboxes/fields in the sidebar** (e.g., "Published Date" from 20150101 to 20241231, "Language: English"), not as inline query syntax. **This is the same mechanism that produced the 36-hit false result in the PubMed run** (extra filters silently stacked alongside Date+Language). Before recording any CINAHL hit count:
1. Run the combined string above with **no limiters applied** first, to get a baseline count.
2. Apply **only** the "Published Date" range (2015–2024) and "Language: English" limiters.
3. Confirm no other limiters (e.g., "Peer Reviewed," "Research Article," age-group, geographic) are checked unless deliberately chosen — re-check the full limiters panel, not just the ones you intentionally set, since EBSCOhost can persist limiter state from a previous unrelated search in the same session.

---

## Known Limitations / Things to Verify Live

1. **CINAHL Subject Heading labels are unverified** (see mapping table above) — "Decision Making, Clinical" is the most likely to need correction.
2. **CINAHL is not a MEDLINE superset** — unlike Embase, expect this string's hit count to be substantially smaller than PubMed's 9,672, and possibly to miss biomedical-engineering-heavy papers that PubMed indexes but CINAHL does not. A low count here is not necessarily a string defect; it may reflect CINAHL's nursing/allied-health editorial scope.
3. **No Emtree-equivalent controlled vocabulary for XAI methods** — Concept A remains free-text-only, same limitation as PubMed (see `search_string_pubmed_v1.md` Known Limitations item 1, re: ANCHOR).
4. **Combined `TI (...) OR AB (...)` blocks are very long** — if EBSCOhost's query parser has a term-count or string-length limit, this may need to be split into multiple search lines (S1 AND S2 style, EBSCOhost's "search history" combination feature) rather than pasted as one block. If a syntax error occurs, try entering Concept A and Concept B as two separate searches (S1, S2) and combining with `S1 AND S2` in the search history.
5. **`#` and `?` wildcards not used** — flag during live testing if any term needs a spelling-variant wildcard (e.g., a future addition with "-ize"/"-ise" forms).

---

## Next Steps

1. Run the Full Combined String (or its split S1/S2 equivalent if needed) live with no limiters; record the baseline hit count.
2. Apply Date (2015–2024) and Language (English) limiters per the verification steps above; record the filtered hit count here and in `data/screening/prisma_counts.csv` (row "Records from database: CINAHL").
3. Resolve the 5 CINAHL Subject Heading candidates via the heading browser; update the mapping table with confirmed labels and re-run if any candidate is missing or substantially changes the count.
4. Check whether PMID 37543055 and/or PMID 32541594 appear in the result set (informational — see Recall validation status above; absence is not disqualifying).
5. Once stable, log the final string, hit count, and any deviations from this draft in `memos/decision_log.md`.

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1 draft (UNTESTED) | 2026-06-09 | Initial field-syntax translation from PubMed v1 rev 3 (9,672 hits). Concept A and B free-text terms converted to `TI (...) OR AB (...)` blocks; 5 MeSH terms mapped to unverified CINAHL Subject Heading candidates. Not yet run live. |
