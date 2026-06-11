# Embase Search String v1 (rev 2 — EM-narrowed) — Clinical XAI Scoping Review (9970)

**Issue:** #22
**Status:** DRAFT / UNTESTED — v2, EM-narrowed (A+B+C). Translated from `search_string_pubmed_v1.md` v2 FINAL (A+B+C: 213 hits 2015-2024 / 497 hits 2015-2026/06/10, live-verified via E-utilities). Supersedes the original v1 cross-domain draft (A+B only, translated from the now-superseded 9,672-hit PubMed cross-domain string). Not yet run against live Embase — hit counts, Emtree term existence, and date/language filter syntax all require live verification.
**Database:** Embase (Embase.com / OvidSP — syntax below targets **Embase.com**; flag platform-specific differences if your institution provides Ovid Embase instead)
**Date range filter (target):** 2015/01/01 through search-execution date (rolling "to present" window — see `memos/decision_log.md`, 2026-06-10. PubMed reference snapshot taken 2026-06-10: A+B+C = 497 hits)
**Language filter (target):** English

---

## Design Rationale

This is a field-syntax translation of the EM-narrowed PubMed v2 FINAL string (`search_string_pubmed_v1.md`). The three-concept AND structure is preserved:

- **Concept A — XAI / Interpretability** (unchanged from the v1 cross-domain translation)
- **Concept B — Clinical / Medical Context** (unchanged from the v1 cross-domain translation)
- **Concept C — Emergency Medicine / ED / Triage / Acuity / Disposition** (NEW for the 2026-06-10 EM pivot)

Concept A and B retain the same translation choices and caveats as the original v1 draft (`:ti,ab,kw` field tag, Emtree candidates marked "to verify" — see those sections below, carried over unchanged from v1). Concept C is new; its translation follows the same `:ti,ab,kw` convention plus two Emtree candidates for the two MeSH terms in the PubMed Concept C block.

**Recall validation status:** unchanged from v1 — the two MEDLINE-indexed benchmark papers (PMID 37543055 — Cao, Kunaprayoon & Ren 2023; PMID 32541594 — Tosun et al. 2020) remain the recommended retrievability test cases, **but neither was validated against Concept C** (they were validated for the cross-domain A+B string). Whether either paper is EM-relevant enough to pass the v2 inclusion boundary (`docs/protocol/inclusion_boundary.md` v2) — and therefore *should* be retrieved by A+B+C — has not been checked. Treat their retrieval as informative but not authoritative for this v2 string; an EM-specific recall benchmark is still pending (see Next Steps).

---

## Concept A — XAI / Interpretability (unchanged from v1)

```
('explainable artificial intelligence':ti,ab,kw OR 'explainable AI':ti,ab,kw OR 'XAI':ti,ab,kw
OR 'interpretable machine learning':ti,ab,kw OR 'interpretability':ti,ab,kw OR 'model interpretability':ti,ab,kw
OR 'explainability':ti,ab,kw OR 'explainable model*':ti,ab,kw
OR 'SHAP':ti,ab,kw OR 'Shapley additive explanation*':ti,ab,kw OR 'Shapley value*':ti,ab,kw
OR 'LIME':ti,ab,kw OR 'local interpretable model-agnostic':ti,ab,kw
OR 'Grad-CAM':ti,ab,kw OR 'gradient-weighted class activation':ti,ab,kw OR 'class activation map*':ti,ab,kw
OR 'counterfactual explanation*':ti,ab,kw
OR 'feature attribution':ti,ab,kw
OR 'rule extraction':ti,ab,kw
OR 'prototype-based explanation':ti,ab,kw OR 'prototype explanation*':ti,ab,kw OR 'case-based explanation*':ti,ab,kw
OR 'interpretable AI':ti,ab,kw OR 'interpretable artificial intelligence':ti,ab,kw
OR 'explainable deep learning':ti,ab,kw)
```

Translation notes carried over unchanged from v1: double quotes -> single quotes (`'...'`), `[tiab]` -> `:ti,ab,kw`, `*` truncation unchanged, optional unverified Emtree candidate `'explainable artificial intelligence'/exp`. **Do not add `'machine learning'/exp` or `'artificial intelligence'/exp`** — see v1 history for the over-broadening (70,946 hits) this caused in PubMed Concept A.

---

## Concept B — Clinical / Medical Context (unchanged from v1)

```
('clinical decision support':ti,ab,kw OR 'clinical decision support system*':ti,ab,kw OR 'CDSS':ti,ab,kw
OR 'computer-aided diagnos*':ti,ab,kw OR 'computer aided diagnos*':ti,ab,kw
OR 'diagnostic algorithm*':ti,ab,kw OR 'predictive model*':ti,ab,kw OR 'risk prediction model*':ti,ab,kw
OR 'clinical':ti,ab,kw OR 'clinician*':ti,ab,kw OR 'physician*':ti,ab,kw OR 'radiolog*':ti,ab,kw
OR 'patholog*':ti,ab,kw OR 'nurse*':ti,ab,kw OR 'diagnosis':ti,ab,kw OR 'diagnostic':ti,ab,kw
OR 'prognosis':ti,ab,kw OR 'treatment':ti,ab,kw OR 'patient care':ti,ab,kw OR 'hospital*':ti,ab,kw
OR 'clinical decision support system'/exp OR 'doctor'/exp
OR 'decision making'/exp OR 'computer assisted diagnosis'/exp
OR 'patient care'/exp)
```

MeSH -> Emtree mapping table (unchanged from v1, still unverified — see Next Steps):

| PubMed MeSH term | Emtree candidate (UNVERIFIED) | Notes |
|---|---|---|
| "Decision Support Systems, Clinical"[Mesh] | `'clinical decision support system'/exp` | Likely a direct match — confirm singular/plural and exact label |
| "Physicians"[Mesh] | `'doctor'/exp` | Emtree's preferred term for this concept is historically "doctor" |
| "Clinical Decision-Making"[Mesh] | `'decision making'/exp` | May be too broad — consider testing without this term first |
| "Diagnosis, Computer-Assisted"[Mesh] | `'computer assisted diagnosis'/exp` | Likely a direct match, confirm hyphenation/spacing |
| "Patient Care"[Mesh] | `'patient care'/exp` | Likely a direct match |

---

## Concept C — Emergency Medicine / ED / Triage / Acuity / Disposition (NEW, 2026-06-10)

```
('emergency department':ti,ab,kw OR 'emergency room':ti,ab,kw OR 'emergency medicine':ti,ab,kw
OR 'emergency severity index':ti,ab,kw OR 'ESI':ti,ab,kw OR 'Triage':ti,ab,kw
OR 'acuity scor*':ti,ab,kw OR 'acuity assessment':ti,ab,kw OR 'acuity level*':ti,ab,kw OR 'acuity classification':ti,ab,kw
OR 'disposition decision*':ti,ab,kw OR 'ED disposition':ti,ab,kw OR 'discharge disposition':ti,ab,kw
OR 'patient intake':ti,ab,kw
OR 'hospital emergency service'/exp OR 'triage'/exp)
```

**Translation notes:**
- Free-text terms translated with the same `[tiab]` -> `:ti,ab,kw` convention as Concepts A and B.
- **MeSH -> Emtree mapping for the 2 controlled-vocabulary terms (UNVERIFIED — confirm via Map Term/thesaurus browser before live execution):**

| PubMed MeSH term | Emtree candidate (UNVERIFIED) | Notes |
|---|---|---|
| "Emergency Service, Hospital"[Mesh] | `'hospital emergency service'/exp` | Emtree's standard heading for ED departments; likely a direct match |
| "Triage"[Mesh] | `'triage'/exp` | Emtree has its own "triage" term; likely a direct match |

- **`'ESI'` and `'Triage'` as bare acronym/word terms carry false-positive risk** — `ESI` is also an abbreviation in unrelated domains (e.g., engineering/electrostatic-discharge literature, which Embase indexes via conference proceedings more than MEDLINE does). If Concept C's contribution to the combined hit count looks disproportionately large relative to the PubMed reference (497), check whether `'ESI':ti,ab,kw` alone is the driver and consider requiring `'emergency severity index'` co-occurrence instead.

---

## Full Combined String (DRAFT — paste into Embase.com search box for first live test)

```
(Concept A) AND (Concept B) AND (Concept C) AND [2015-<SEARCH-EXECUTION-DATE>]/py AND [english]/lim
```

```
('explainable artificial intelligence':ti,ab,kw OR 'explainable AI':ti,ab,kw OR 'XAI':ti,ab,kw OR 'interpretable machine learning':ti,ab,kw OR 'interpretability':ti,ab,kw OR 'model interpretability':ti,ab,kw OR 'explainability':ti,ab,kw OR 'explainable model*':ti,ab,kw OR 'SHAP':ti,ab,kw OR 'Shapley additive explanation*':ti,ab,kw OR 'Shapley value*':ti,ab,kw OR 'LIME':ti,ab,kw OR 'local interpretable model-agnostic':ti,ab,kw OR 'Grad-CAM':ti,ab,kw OR 'gradient-weighted class activation':ti,ab,kw OR 'class activation map*':ti,ab,kw OR 'counterfactual explanation*':ti,ab,kw OR 'feature attribution':ti,ab,kw OR 'rule extraction':ti,ab,kw OR 'prototype-based explanation':ti,ab,kw OR 'prototype explanation*':ti,ab,kw OR 'case-based explanation*':ti,ab,kw OR 'interpretable AI':ti,ab,kw OR 'interpretable artificial intelligence':ti,ab,kw OR 'explainable deep learning':ti,ab,kw)
AND
('clinical decision support':ti,ab,kw OR 'clinical decision support system*':ti,ab,kw OR 'CDSS':ti,ab,kw OR 'computer-aided diagnos*':ti,ab,kw OR 'computer aided diagnos*':ti,ab,kw OR 'diagnostic algorithm*':ti,ab,kw OR 'predictive model*':ti,ab,kw OR 'risk prediction model*':ti,ab,kw OR 'clinical':ti,ab,kw OR 'clinician*':ti,ab,kw OR 'physician*':ti,ab,kw OR 'radiolog*':ti,ab,kw OR 'patholog*':ti,ab,kw OR 'nurse*':ti,ab,kw OR 'diagnosis':ti,ab,kw OR 'diagnostic':ti,ab,kw OR 'prognosis':ti,ab,kw OR 'treatment':ti,ab,kw OR 'patient care':ti,ab,kw OR 'hospital*':ti,ab,kw OR 'clinical decision support system'/exp OR 'doctor'/exp OR 'decision making'/exp OR 'computer assisted diagnosis'/exp OR 'patient care'/exp)
AND
('emergency department':ti,ab,kw OR 'emergency room':ti,ab,kw OR 'emergency medicine':ti,ab,kw OR 'emergency severity index':ti,ab,kw OR 'ESI':ti,ab,kw OR 'Triage':ti,ab,kw OR 'acuity scor*':ti,ab,kw OR 'acuity assessment':ti,ab,kw OR 'acuity level*':ti,ab,kw OR 'acuity classification':ti,ab,kw OR 'disposition decision*':ti,ab,kw OR 'ED disposition':ti,ab,kw OR 'discharge disposition':ti,ab,kw OR 'patient intake':ti,ab,kw OR 'hospital emergency service'/exp OR 'triage'/exp)
AND [2015-<SEARCH-EXECUTION-DATE>]/py
AND [english]/lim
```

**Date range note:** `<SEARCH-EXECUTION-DATE>` is a placeholder — substitute the actual date the search is run (e.g., `[2015-2026]/py` if Embase's `/py` syntax only supports year granularity; check whether a finer-grained date-of-publication range is available via the Limits sidebar for the partial current year). This rolling-to-present range was decided 2026-06-10 (`memos/decision_log.md`) — re-run at the actual execution date and record the count obtained then, not the 2026-06-10 PubMed reference snapshot (497).

**Date/language syntax caveat — read before running** (unchanged from v1): `[2015-<date>]/py` and `[english]/lim` are standard Embase.com inline-query syntax, but Embase.com's "Limits" sidebar can silently stack additional filters (document type, age group, etc.) — this is exactly the mechanism that produced the 36-hit false result during PubMed v1 development. Before recording any Embase hit count, confirm via the Limits/sidebar panel that **only** Date of Publication and Language (English) are active.

---

## Known Limitations / Things to Verify Live

1. **Platform ambiguity (Embase.com vs. Ovid Embase)** — unchanged from v1; determine which platform your institution provides before the first live run, as it changes nearly every line of this document.
2. **Emtree term existence and scope are entirely unverified** for both Concept B (5 candidates) and Concept C (2 candidates, NEW) — the single biggest source of uncertainty in this draft.
3. **`:ti,ab,kw` vs. `:ti,ab`** — if the hit count is dramatically higher than the PubMed reference (497), consider testing `:ti,ab` (drop author keywords) as a precision check.
4. **Embase indexes conference proceedings and abstracts more heavily than MEDLINE** — expect a higher proportion of conference-abstract-only records, which may need a publication-type flag at screening (E4 in `docs/protocol/screening_criteria.md`).
5. **No EM-specific retrievability benchmark exists yet** (see Design Rationale) — the two MEDLINE-indexed benchmark papers carried over from v1 were validated against the cross-domain A+B string, not A+B+C.
6. **Rolling date range** — `/py` is a publication-year filter; if Embase requires full-year granularity (i.e., cannot express "through 2026-06-10" and only "through 2026"), the live-executed count will include all of 2026 to date, including ahead-of-print 2026 records that could later be reclassified — consistent with the Epub-ahead-of-print caveat discussed for the PubMed string in `memos/decision_log.md` (2026-06-10 entry).

---

## Next Steps

1. Confirm Embase.com vs. Ovid Embase platform for institutional access.
2. Run the Full Combined String (A+B+C, with `<SEARCH-EXECUTION-DATE>` substituted for the actual execution date) live; record the raw hit count here and in `data/screening/prisma_counts.csv` (row "Records from database: Embase").
3. Resolve the 7 Emtree candidates (5 from Concept B, 2 from Concept C) via Map Term/thesaurus browser; update both mapping tables with confirmed labels and re-run if any candidate is missing or substantially changes the count.
4. Compare the resulting hit count against the PubMed A+B+C reference (213 @ 2015-2024 / 497 @ 2015-2026/06/10) — large deviations in either direction warrant the precision checks in Known Limitations items 3 and 6.
5. Once stable, log the final string, hit count, and any deviations from this draft in `memos/decision_log.md`.

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1 draft (UNTESTED) | 2026-06-09 | Initial field-syntax translation from PubMed cross-domain v1 rev 3 (9,672 hits, A+B only). Concept A and B free-text terms converted to `:ti,ab,kw`; 5 MeSH terms mapped to unverified Emtree candidates. Not yet run live. |
| v2 draft (UNTESTED, EM-narrowed) | 2026-06-10 | EM pivot: Concept C (ED/triage/ESI/acuity/disposition, free text + 2 Emtree candidates) added; restructured to A+B+C; date range extended from fixed 2015-2024 to rolling "2015 through search-execution date" per `memos/decision_log.md` (2026-06-10). Translated from PubMed v2 FINAL (A+B+C: 213 hits @ 2015-2024 / 497 hits @ 2015-2026/06/10). Not yet run live. |
