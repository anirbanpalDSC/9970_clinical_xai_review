# IEEE Xplore Search String v1 (rev 2 — EM-narrowed) — Clinical XAI Scoping Review (9970)

**Issue:** #22
**Status:** DRAFT / UNTESTED — v2, EM-narrowed (A+B+C). Translated from `search_string_pubmed_v1.md` v2 FINAL (A+B+C: 213 hits 2015-2024 / 497 hits 2015-2026/06/10, live-verified via E-utilities). Supersedes the original v1 cross-domain draft (A+B only, translated from the now-superseded 9,672-hit PubMed cross-domain string). Not yet run against live IEEE Xplore.
**Database:** IEEE Xplore Digital Library (Command Search)
**Date range filter (target):** 2015/01/01 through search-execution date (rolling "to present" window — see `memos/decision_log.md`, 2026-06-10. PubMed reference snapshot taken 2026-06-10: A+B+C = 497 hits)
**Language filter (target):** English (no separate language field in IEEE Xplore — see Known Limitations)

---

## Design Rationale

This is a field-syntax translation of the EM-narrowed PubMed v2 FINAL string (`search_string_pubmed_v1.md`). The three-concept AND structure is preserved:

- **Concept A — XAI / Interpretability** (unchanged from the v1 cross-domain translation)
- **Concept B — Clinical / Medical Context** (unchanged from the v1 cross-domain translation; 5 MeSH terms dropped, free-text only — see v1 history)
- **Concept C — Emergency Medicine / ED / Triage / Acuity / Disposition** (NEW for the 2026-06-10 EM pivot; both MeSH-equivalent terms in the PubMed Concept C block — "Emergency Service, Hospital" and "Triage" — are dropped as controlled vocabulary, consistent with Concept B's treatment, but "Triage" survives as a free-text term)

**Recall validation status — unchanged from v1: IEEE has no confirmed benchmark paper.** None of the four non-MEDLINE benchmark papers identified during PubMed validation are IEEE venues (see v1 Design Rationale for the full list). **If full-text screening later identifies an included paper published in IEEE Transactions on Medical Imaging, IEEE JBHI, or another IEEE venue, retroactively confirm this string retrieves it** and log the result.

---

## Concept A — XAI / Interpretability (unchanged from v1, free-text only)

```
("explainable artificial intelligence" OR "explainable AI" OR XAI
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
OR "explainable deep learning")
```

---

## Concept B — Clinical / Medical Context (unchanged from v1, free-text only — MeSH terms dropped)

```
("clinical decision support" OR "clinical decision support system*" OR CDSS
OR "computer-aided diagnos*" OR "computer aided diagnos*"
OR "diagnostic algorithm*" OR "predictive model*" OR "risk prediction model*"
OR clinical OR "clinician*" OR "physician*" OR "radiolog*"
OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic
OR prognosis OR treatment OR "patient care" OR "hospital*")
```

---

## Concept C — Emergency Medicine / ED / Triage / Acuity / Disposition (NEW, 2026-06-10, free-text only)

```
("emergency department" OR "emergency room" OR "emergency medicine"
OR "emergency severity index" OR ESI OR Triage
OR "acuity scor*" OR "acuity assessment" OR "acuity level*" OR "acuity classification"
OR "disposition decision*" OR "ED disposition" OR "discharge disposition"
OR "patient intake")
```

**Translation notes:**
- The PubMed Concept C block's 2 MeSH terms ("Emergency Service, Hospital"[Mesh], "Triage"[Mesh]) are dropped as controlled vocabulary — IEEE has no clinical thesaurus equivalent (same situation as Concept B's 5 dropped MeSH terms). `Triage` as a free-text term already covers the bulk of the "Triage"[Mesh] concept.
- **`ESI` and `Triage` as bare terms carry false-positive risk in IEEE's engineering-heavy corpus** — `ESI` in particular is a common acronym in electronics/signal-processing literature unrelated to the Emergency Severity Index. If Concept C looks like it is contributing a disproportionate number of off-topic hits, consider requiring `"emergency severity index"` (full phrase) instead of bare `ESI`.

---

## Full Combined String — Option 1 (RECOMMENDED FIRST TEST: unrestricted Command Search)

```
(Concept A) AND (Concept B) AND (Concept C)
```

```
("explainable artificial intelligence" OR "explainable AI" OR XAI OR "interpretable machine learning" OR interpretability OR "model interpretability" OR explainability OR "explainable model*" OR SHAP OR "Shapley additive explanation*" OR "Shapley value*" OR LIME OR "local interpretable model-agnostic" OR "Grad-CAM" OR "gradient-weighted class activation" OR "class activation map*" OR "counterfactual explanation*" OR "feature attribution" OR "rule extraction" OR "prototype-based explanation" OR "prototype explanation*" OR "case-based explanation*" OR "interpretable AI" OR "interpretable artificial intelligence" OR "explainable deep learning")
AND
("clinical decision support" OR "clinical decision support system*" OR CDSS OR "computer-aided diagnos*" OR "computer aided diagnos*" OR "diagnostic algorithm*" OR "predictive model*" OR "risk prediction model*" OR clinical OR "clinician*" OR "physician*" OR "radiolog*" OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic OR prognosis OR treatment OR "patient care" OR "hospital*")
AND
("emergency department" OR "emergency room" OR "emergency medicine" OR "emergency severity index" OR ESI OR Triage OR "acuity scor*" OR "acuity assessment" OR "acuity level*" OR "acuity classification" OR "disposition decision*" OR "ED disposition" OR "discharge disposition" OR "patient intake")
```

Paste this directly into the **Command Search** box at ieeexplore.ieee.org. With no field tags, IEEE Xplore searches **"Full Text & Metadata"** by default. Adding Concept C narrows the cross-domain Option 1 baseline considerably (the PubMed analogue dropped from 9,672 to 213-497), but the "Full Text & Metadata" scope means this is still likely an **upper-bound baseline**, not a final count — see Known Limitations item 3.

---

## Full Combined String — Option 2 (precision-restricted: Document Title + Abstract + Author Keywords)

```
(("Document Title":(Concept A) OR "Abstract":(Concept A) OR "Author Keywords":(Concept A)))
AND
(("Document Title":(Concept B) OR "Abstract":(Concept B) OR "Author Keywords":(Concept B)))
AND
(("Document Title":(Concept C) OR "Abstract":(Concept C) OR "Author Keywords":(Concept C)))
```

where `(Concept A)`, `(Concept B)`, `(Concept C)` are the three parenthesized OR-blocks defined above, substituted in place of each placeholder. The field-tag-group syntax verification approach is unchanged from v1 — test with the small fragment `"Document Title":(XAI OR "explainable AI")` first (see v1 Known Limitations item 4 for the per-term-repeated fallback if it errors).

---

## Known Limitations / Things to Verify Live

1. **No language filter field** — unchanged from v1; handle at screening if needed.
2. **Year range filter is UI/sidebar-based, now rolling "to present"** — apply 2015 through the actual search-execution date via the "Year" facet. **Same filter-stacking caution as the PubMed 36-hit incident**: confirm no other facets (Content Type, Publisher, etc.) are inadvertently applied. Because the upper bound is "now" rather than a fixed past year, very-recent 2025-2026 IEEE Xplore "Early Access" articles may appear — note whether IEEE's "Early Access" status is analogous to PubMed's Epub-ahead-of-print (`memos/decision_log.md`, 2026-06-10) and whether such articles should be included or flagged for re-check at execution time.
3. **Option 1's "Full Text & Metadata" default scope is a major precision risk** — unchanged from v1. Adding Concept C should reduce the absolute hit count substantially (in proportion to the PubMed 9,672 -> 213-497 narrowing), but if Option 1's count is still enormous, Option 2 is likely necessary.
4. **Option 2's field-tag-group syntax is unverified** — unchanged from v1, now applies to 3 concepts (9 field-tagged clauses) instead of 2 (6 clauses).
5. **No controlled vocabulary for any of the three concepts** — unchanged from v1; this remains the most precision-fragile of the database translations.
6. **No EM-specific retrievability benchmark** — unchanged from v1 (see Design Rationale).

---

## Next Steps

1. Run **Option 1** (unrestricted Command Search, A+B+C) live; record the raw hit count as a baseline and compare against the PubMed A+B+C reference (213 @ 2015-2024 / 497 @ 2015-2026/06/10).
2. Test the small Option 2 fragment to determine whether field-tag-group syntax works; build the full Option 2 string (or per-term fallback) accordingly.
3. Apply the Year filter (2015 through the actual search-execution date), confirming no other facets are stacked, and noting any "Early Access" articles per Known Limitations item 2.
4. Record the final hit count here and in `data/screening/prisma_counts.csv` (row "Records from database: IEEE Xplore").
5. Once stable, log the final string, hit count, and the chosen Option (1 vs. 2) in `memos/decision_log.md`.
6. Flag for the manuscript: no IEEE-specific retrievability benchmark exists yet — retroactively validate against any IEEE-published paper that survives full-text screening.

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1 draft (UNTESTED) | 2026-06-09 | Initial translation from PubMed cross-domain v1 rev 3 (9,672 hits, A+B only). 5 MeSH terms dropped (no IEEE equivalent); two candidate query forms provided (Option 1: unrestricted baseline; Option 2: field-restricted, syntax unverified). Not yet run live. |
| v2 draft (UNTESTED, EM-narrowed) | 2026-06-10 | EM pivot: Concept C (ED/triage/ESI/acuity/disposition, free text only) added to both Options 1 and 2; date range extended from fixed 2015-2024 to rolling "2015 through search-execution date" per `memos/decision_log.md` (2026-06-10). Translated from PubMed v2 FINAL (A+B+C: 213 hits @ 2015-2024 / 497 hits @ 2015-2026/06/10). Not yet run live. |
