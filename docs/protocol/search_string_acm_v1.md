# ACM Digital Library Search String v1 (rev 2 — EM-narrowed) — Clinical XAI Scoping Review (9970)

**Issue:** #22
**Status:** **EXECUTED (2026-06-22) — 1 record, via a documented methodology substitution.** The bracket-nested field-query syntax below (`[Title: (...)] OR [Abstract: (...)] OR [Keyword: (...)]`) was tested live against ACM's native Advanced Search (dl.acm.org/search/advanced) and returned **0 results — including for single-term control queries** (`[Title: "machine learning"]` alone), ruling out a translation/term problem and pointing to either a UI-only display syntax that isn't valid raw input, or a more basic access issue. After 3 failed attempts to recover ACM's native query syntax, the search was executed instead via the **OpenAlex API** (api.openalex.org), restricted to ACM as publisher, using the same wildcard-fixed term lists. See "Methodology Substitution (2026-06-22)" section below for the full rationale, query, and result. Translated from `search_string_pubmed_v1.md` v2 FINAL (A+B+C: 213 hits 2015-2024 / 497 hits 2015-2026/06/10, live-verified via E-utilities). Supersedes the original v1 cross-domain draft (A+B only, translated from the now-superseded 9,672-hit PubMed cross-domain string).
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
OR explainability OR "explainable model" OR "explainable models"
OR SHAP OR "Shapley additive explanation" OR "Shapley additive explanations" OR "Shapley value" OR "Shapley values"
OR LIME OR "local interpretable model-agnostic"
OR "Grad-CAM" OR "gradient-weighted class activation" OR "class activation map" OR "class activation maps" OR "class activation mapping"
OR "counterfactual explanation" OR "counterfactual explanations"
OR "feature attribution"
OR "rule extraction"
OR "prototype-based explanation" OR "prototype explanation" OR "prototype explanations" OR "case-based explanation" OR "case-based explanations"
OR "interpretable AI" OR "interpretable artificial intelligence"
OR "explainable deep learning"
```

**Wildcard-limit pre-fix (2026-06-18):** all 7 wildcarded terms originally in this block (`explainable model*`, `Shapley additive explanation*`, `Shapley value*`, `class activation map*`, `counterfactual explanation*`, `prototype explanation*`, `case-based explanation*`) had small, predictable suffix sets and were enumerated explicitly as a precaution — see Known Limitations item 8 below. (Truncation verification status for the remaining bare-word terms is otherwise unchanged from v1.)

---

## Concept B — Clinical / Medical Context (unchanged from v1, free-text only — MeSH terms dropped)

```
"clinical decision support" OR "clinical decision support system" OR "clinical decision support systems" OR CDSS
OR "computer-aided diagnos*" OR "computer aided diagnos*"
OR "diagnostic algorithm" OR "diagnostic algorithms" OR "predictive model" OR "predictive models" OR "risk prediction model" OR "risk prediction models"
OR clinical OR clinician OR clinicians OR physician OR physicians OR "radiolog*"
OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic
OR prognosis OR treatment OR "patient care" OR "hospital*"
```

**Wildcard-limit pre-fix (2026-06-18):** of the 12 wildcarded terms originally in this block, 6 with small/predictable suffix sets (`clinical decision support system*`, `diagnostic algorithm*`, `predictive model*`, `risk prediction model*`, `clinician*`, `physician*`) were enumerated explicitly. The remaining 6 — single-word stems with unpredictable/numerous suffix forms (`computer-aided diagnos*`, `computer aided diagnos*`, `radiolog*`, `patholog*`, `nurse*`, `hospital*`) — keep the wildcard. See Known Limitations item 8 below.

---

## Concept C — Emergency Medicine / ED / Triage / Acuity / Disposition (NEW, 2026-06-10, free-text only)

```
"emergency department" OR "emergency room" OR "emergency medicine"
OR "emergency severity index" OR ESI OR Triage
OR "acuity score" OR "acuity scores" OR "acuity scoring" OR "acuity assessment" OR "acuity level" OR "acuity levels" OR "acuity classification"
OR "disposition decision" OR "disposition decisions" OR "ED disposition" OR "discharge disposition"
OR "patient intake"
```

**Wildcard-limit pre-fix (2026-06-18):** all 3 wildcarded terms originally in this block (`acuity scor*`, `acuity level*`, `disposition decision*`) had small, predictable suffix sets and were enumerated explicitly. See Known Limitations item 8 below.

**Translation notes:**
- The 2 MeSH-equivalent terms from the PubMed Concept C block are dropped — same rationale as Concept B (no ACM CCS clinical vocabulary). `Triage` as a free-text term covers most of the dropped "Triage"[Mesh] concept.
- These three terms were originally wildcarded (`"acuity scor*"`, `"acuity level*"`, `"disposition decision*"`) but were enumerated as explicit word forms in the 2026-06-18 wildcard-limit pre-fix (see note above) — no truncation-behavior verification needed for this block.
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
[[Title: ("explainable artificial intelligence" OR "explainable AI" OR XAI OR "interpretable machine learning" OR interpretability OR "model interpretability" OR explainability OR "explainable model" OR "explainable models" OR SHAP OR "Shapley additive explanation" OR "Shapley additive explanations" OR "Shapley value" OR "Shapley values" OR LIME OR "local interpretable model-agnostic" OR "Grad-CAM" OR "gradient-weighted class activation" OR "class activation map" OR "class activation maps" OR "class activation mapping" OR "counterfactual explanation" OR "counterfactual explanations" OR "feature attribution" OR "rule extraction" OR "prototype-based explanation" OR "prototype explanation" OR "prototype explanations" OR "case-based explanation" OR "case-based explanations" OR "interpretable AI" OR "interpretable artificial intelligence" OR "explainable deep learning")]
OR [Abstract: ("explainable artificial intelligence" OR "explainable AI" OR XAI OR "interpretable machine learning" OR interpretability OR "model interpretability" OR explainability OR "explainable model" OR "explainable models" OR SHAP OR "Shapley additive explanation" OR "Shapley additive explanations" OR "Shapley value" OR "Shapley values" OR LIME OR "local interpretable model-agnostic" OR "Grad-CAM" OR "gradient-weighted class activation" OR "class activation map" OR "class activation maps" OR "class activation mapping" OR "counterfactual explanation" OR "counterfactual explanations" OR "feature attribution" OR "rule extraction" OR "prototype-based explanation" OR "prototype explanation" OR "prototype explanations" OR "case-based explanation" OR "case-based explanations" OR "interpretable AI" OR "interpretable artificial intelligence" OR "explainable deep learning")]
OR [Keyword: ("explainable artificial intelligence" OR "explainable AI" OR XAI OR "interpretable machine learning" OR interpretability OR "model interpretability" OR explainability OR "explainable model" OR "explainable models" OR SHAP OR "Shapley additive explanation" OR "Shapley additive explanations" OR "Shapley value" OR "Shapley values" OR LIME OR "local interpretable model-agnostic" OR "Grad-CAM" OR "gradient-weighted class activation" OR "class activation map" OR "class activation maps" OR "class activation mapping" OR "counterfactual explanation" OR "counterfactual explanations" OR "feature attribution" OR "rule extraction" OR "prototype-based explanation" OR "prototype explanation" OR "prototype explanations" OR "case-based explanation" OR "case-based explanations" OR "interpretable AI" OR "interpretable artificial intelligence" OR "explainable deep learning")]]
AND
[[Title: ("clinical decision support" OR "clinical decision support system" OR "clinical decision support systems" OR CDSS OR "computer-aided diagnos*" OR "computer aided diagnos*" OR "diagnostic algorithm" OR "diagnostic algorithms" OR "predictive model" OR "predictive models" OR "risk prediction model" OR "risk prediction models" OR clinical OR clinician OR clinicians OR physician OR physicians OR "radiolog*" OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic OR prognosis OR treatment OR "patient care" OR "hospital*")]
OR [Abstract: ("clinical decision support" OR "clinical decision support system" OR "clinical decision support systems" OR CDSS OR "computer-aided diagnos*" OR "computer aided diagnos*" OR "diagnostic algorithm" OR "diagnostic algorithms" OR "predictive model" OR "predictive models" OR "risk prediction model" OR "risk prediction models" OR clinical OR clinician OR clinicians OR physician OR physicians OR "radiolog*" OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic OR prognosis OR treatment OR "patient care" OR "hospital*")]
OR [Keyword: ("clinical decision support" OR "clinical decision support system" OR "clinical decision support systems" OR CDSS OR "computer-aided diagnos*" OR "computer aided diagnos*" OR "diagnostic algorithm" OR "diagnostic algorithms" OR "predictive model" OR "predictive models" OR "risk prediction model" OR "risk prediction models" OR clinical OR clinician OR clinicians OR physician OR physicians OR "radiolog*" OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic OR prognosis OR treatment OR "patient care" OR "hospital*")]]
AND
[[Title: ("emergency department" OR "emergency room" OR "emergency medicine" OR "emergency severity index" OR ESI OR Triage OR "acuity score" OR "acuity scores" OR "acuity scoring" OR "acuity assessment" OR "acuity level" OR "acuity levels" OR "acuity classification" OR "disposition decision" OR "disposition decisions" OR "ED disposition" OR "discharge disposition" OR "patient intake")]
OR [Abstract: ("emergency department" OR "emergency room" OR "emergency medicine" OR "emergency severity index" OR ESI OR Triage OR "acuity score" OR "acuity scores" OR "acuity scoring" OR "acuity assessment" OR "acuity level" OR "acuity levels" OR "acuity classification" OR "disposition decision" OR "disposition decisions" OR "ED disposition" OR "discharge disposition" OR "patient intake")]
OR [Keyword: ("emergency department" OR "emergency room" OR "emergency medicine" OR "emergency severity index" OR ESI OR Triage OR "acuity score" OR "acuity scores" OR "acuity scoring" OR "acuity assessment" OR "acuity level" OR "acuity levels" OR "acuity classification" OR "disposition decision" OR "disposition decisions" OR "ED disposition" OR "discharge disposition" OR "patient intake")]]
```

**Wildcard multiplier caution:** the 6 wildcards retained in Concept B (`computer-aided diagnos*`, `computer aided diagnos*`, `radiolog*`, `patholog*`, `nurse*`, `hospital*`) each appear once per field bracket (Title, Abstract, Keyword) in this combined string — i.e. **18 wildcard occurrences total**, not 6, once the per-concept block is repeated three times. If ACM DL enforces a wildcard cap counted across the whole query string (rather than per-bracket), this combined string could still be rejected even though each individual concept block only has 6. **Test the small Option-2-style fragment first** (Next Steps item 2/3) before running the full combined string, and be ready to reduce further (e.g. drop `nurse*`/`hospital*` to bare non-wildcard `nurse`/`hospital` if the test fails) — see Known Limitations item 8.

**Date filter:** apply 2015 through the actual search-execution date via the **"Publication Date"** facet/filter (custom range option) — rolling "to present" per `memos/decision_log.md` (2026-06-10), not a fixed 2015-2024 range. Same filter-stacking caution as v1: check the full facet panel for any other filters carried over from a previous session.

**This bracket-nested string was tested live on 2026-06-22 and failed — see Methodology Substitution section immediately below for what was used instead.**

---

## Methodology Substitution (2026-06-22) — EXECUTED via OpenAlex API

**What happened:** the Full Combined String above was pasted into ACM's Advanced Search ("Edit Query") box at dl.acm.org/search/advanced and returned **0 results**. To isolate whether this was a translation problem (wrong terms) or a syntax problem (wrong query format), three diagnostic fragments were tested:
1. `[Title: "machine learning"]` — single bracketed term, no OR — **0 results**
2. `[Title: "machine learning"] OR [Title: "deep learning"]` — OR across two brackets — **0 results**

Both returned 0 despite "machine learning" being a near-certain high-volume term in ACM titles, ruling out a term/translation issue. The most likely explanation: the `[Field: (...)]` bracket notation is a **UI-only display format** that ACM's Advanced Search shows you after building a query through the form-based builder, not literal paste-able syntax for the raw query box. After 3 failed attempts, further guessing at ACM's native syntax was abandoned in favor of a working alternative.

**Substitution:** ACM Digital Library has no public, official search API (unlike PubMed's E-utilities or IEEE Xplore's Metadata API). Instead, the search was executed against **OpenAlex** (api.openalex.org) — a free, public, well-documented scholarly index that includes ACM's catalog — restricted to ACM as publisher. This is a different system than ACM's own search engine (OpenAlex indexes ACM's metadata/abstracts via Crossref-deposited data, not ACM's native full-text index), so it is logged as a documented methodology substitution, the same way Embase's access gap was logged, rather than presented as equivalent to the originally planned native-UI search.

**Verification performed before trusting the result:**
- Confirmed ACM's OpenAlex publisher ID (`P4310319798`, 166,548 total works) via the `/publishers?search=...` endpoint — not guessed.
- Confirmed boolean OR (`|`-separated), AND-across-concepts (comma-separated repeated `title_and_abstract.search.exact` filters), wildcard truncation (`radiolog*` etc., via the `.exact` unstemmed field), year-range, and language filters each work individually via small test queries before assembling the full query.
- Checked abstract coverage for the corpus being searched: **63,606 / 64,974 (97.9%) of ACM works (2015–2026) have an abstract indexed in OpenAlex** — i.e., the recall risk from missing abstracts is low but non-zero (~2% of the corpus has title-only matching available).

**Query executed** (filter parameter, URL-encoded when sent; `<Concept A/B/C>` are the same term lists as the sections above, `|`-separated with multi-word phrases quoted instead of " OR "):

```
primary_location.source.host_organization:P4310319798,
language:en,
publication_year:2015-2026,
title_and_abstract.search.exact:<Concept A terms, pipe-separated>,
title_and_abstract.search.exact:<Concept B terms, pipe-separated>,
title_and_abstract.search.exact:<Concept C terms, pipe-separated>
```

**Result: 1 record.** DOI `10.1145/3453166` — "Triage of 2D Mammographic Images Using Multi-view Multi-task Convolutional Neural Networks" (2021).

**Diagnostic breakdown** (same incremental-narrowing check used for the PubMed string):

| Query | Hit count |
|---|---|
| Concept A alone (any ACM paper) | 773 |
| Concept C alone (any ACM paper) | 32 |
| Concept A AND Concept C | 1 |
| Concept A AND Concept B AND Concept C | 1 |

Concept C (EM-specific terms) is the binding constraint, not Concept B — consistent with this doc's own Design Rationale prediction that ACM's CS/HCI-heavy corpus might yield "few or no additional hits beyond A+B... a plausible and informative null result, not necessarily a translation error."

**Screening-relevance note:** the single hit is an image-triage/prioritization paper in a radiology/mammography screening pipeline, not an ED patient-encounter disposition decision. It is very likely to fail Gate 1 of the EM inclusion boundary (`docs/protocol/inclusion_boundary.md` v2) at full-text screening — i.e., the practical ACM contribution to the final included-studies set may be **zero**, even though 1 record is recorded for PRISMA Identification accounting. This is retained rather than pre-filtered, consistent with how Gate 1 exclusions are handled for every other database.

**Raw export:** `data/searches/acm_openalex_2026-06-22_1.json` (query parameters, diagnostic breakdown, and the single result record).

---

## Known Limitations / Things to Verify Live

1. **Bracket-nesting custom query syntax is unverified** — unchanged from v1, now with a third `[Field: (...)]` triplet for Concept C.
2. **Wildcard (`*`) behaviour is unverified** — unchanged from v1; the 2026-06-18 pre-fix (item 8) reduced Concept C's wildcard count to zero and Concept A's to zero, leaving only Concept B's 6 retained stems to verify.
3. **No language filter** — unchanged from v1.
4. **No proximity operators** — unchanged from v1.
5. **`Keyword` field scope** — unchanged from v1.
6. **Both MeSH-equivalent terms dropped from Concept C** — same situation and rationale as Concept B's 5 dropped MeSH terms.
7. **Retrievability test cases (Kumar et al., Gu et al.) may legitimately fail Concept C** — see Design Rationale; do not treat their absence from the A+B+C result set as a translation error without first checking whether they pass the v2 EM inclusion boundary (`docs/protocol/inclusion_boundary.md` v2) at all.
8. **Wildcard cap unconfirmed for ACM DL (pre-fix applied 2026-06-18)** — IEEE Xplore's Command Search rejected the equivalent translation at 22 wildcards (limit: 10; see `docs/protocol/search_string_ieee_v1.md`). As a precaution, this string was pre-emptively reduced from 22 to 6 wildcarded terms per concept-block (16 enumerated as explicit word-form `OR` clauses). **However, the bracket-nested Title/Abstract/Keyword structure repeats Concept B's 6 retained wildcards three times — 18 occurrences in the full combined string**, not 6 — so this string may still trip a whole-query wildcard cap if ACM DL has one. Test incrementally (Next Steps items 2-3) rather than pasting the full combined string on the first attempt.

---

## Next Steps

1. ~~Sanity-check: search ACM DL by title for "Doctor's Dilemma" (Kumar et al. 2021) and "xPath" (Gu et al.)~~ Superseded — native ACM DL search abandoned after the bracket syntax failed control-term testing (see Methodology Substitution section).
2. ~~Build the Concept A + B + C search via the Advanced Search UI form~~ Superseded — executed via OpenAlex API instead (see Methodology Substitution section).
3. ~~Test wildcard behaviour~~ Done, against OpenAlex's `.search.exact` field — confirmed working.
4. ~~Run the Full Combined String (A+B+C)~~ Done (2026-06-22) — **1 record**, via OpenAlex. See Methodology Substitution section for the diagnostic breakdown and Kumar/Gu-equivalent screening-relevance note.
5. ~~Apply the Publication Date filter~~ Done — 2015-2026, applied via OpenAlex's `publication_year` filter.
6. ~~Record the final hit count here and in `data/screening/prisma_counts.csv`~~ Done (2026-06-22).
7. Log the methodology substitution and result in `memos/decision_log.md`.
8. If time allows later in the project, revisit ACM's native Advanced Search UI (e.g., by building a query through the form rather than a raw text box) to cross-check the OpenAlex result — not required to proceed, but would strengthen the methods section if resolved.

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1 draft (UNTESTED) | 2026-06-09 | Initial translation from PubMed cross-domain v1 rev 3 (9,672 hits, A+B only). 5 MeSH terms dropped (no ACM CCS equivalent); bracket-nested `[Field: (...)]` custom query syntax proposed but unverified; Kumar et al. (2021) and Gu et al. (2020/2023) identified as primary retrievability test cases. Not yet run live. |
| v2 draft (UNTESTED, EM-narrowed) | 2026-06-10 | EM pivot: Concept C (ED/triage/ESI/acuity/disposition, free text only) added; restructured to A+B+C; date range extended from fixed 2015-2024 to rolling "2015 through search-execution date" per `memos/decision_log.md` (2026-06-10). Translated from PubMed v2 FINAL (A+B+C: 213 hits @ 2015-2024 / 497 hits @ 2015-2026/06/10). Noted that Kumar et al./Gu et al. retrievability test cases may legitimately fail Concept C under the v2 EM inclusion boundary. Not yet run live. |
| v2 — wildcard-limit pre-fix (UNTESTED) | 2026-06-18 | Pre-emptively applied the same wildcard reduction discovered on IEEE Xplore (10-wildcard cap): 22 wildcarded terms reduced to 6 per concept-block by enumerating 16 predictable word-form variants explicitly. Flagged that the bracket-nested Title/Abstract/Keyword structure triples Concept B's 6 retained wildcards to 18 occurrences in the full combined string — a whole-query cap (if ACM DL has one) may still be tripped; recommended incremental testing. Not yet run live. |
| v2 — EXECUTED via OpenAlex methodology substitution | 2026-06-22 | Native ACM DL Advanced Search bracket syntax tested live and rejected (0 results, including for single-term control queries — ruled out translation error, pointed to invalid/UI-only syntax). After 3 failed attempts, executed instead via the OpenAlex API restricted to ACM as publisher, using the same wildcard-fixed term lists. **Result: 1 record** (DOI 10.1145/3453166), likely to fail Gate 1 of the EM inclusion boundary at full-text screening. Diagnostic breakdown: Concept A alone = 773, Concept C alone = 32, A+C = 1, A+B+C = 1 (Concept C is the binding constraint, as this doc's Design Rationale anticipated). Logged as a documented methodology substitution in `memos/decision_log.md` and `docs/osf/preregistration_draft.md`. Raw export: `data/searches/acm_openalex_2026-06-22_1.json`. `data/screening/prisma_counts.csv` updated. |
