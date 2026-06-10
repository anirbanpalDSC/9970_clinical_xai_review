# Embase Search String v1 — Clinical XAI Systematic Review (9970)

**Issue:** #22
**Status:** DRAFT / UNTESTED — translated from the validated PubMed v1 rev 3 string (`search_string_pubmed_v1.md`, 9,672 hits). Not yet run against live Embase. Hit counts, Emtree term existence, and date/language filter syntax all require live verification.
**Database:** Embase (Embase.com / OvidSP — syntax below targets **Embase.com**; flag platform-specific differences if your institution provides Ovid Embase instead)
**Date range filter (target):** 2015–2024
**Language filter (target):** English

---

## Design Rationale

This is a field-syntax translation of the finalized PubMed v1 rev 3 string (see `search_string_pubmed_v1.md` for the full diagnostic history: 9 → 36 → 15,385 → 9,672 hits). The same two-concept AND structure is preserved:

- **Concept A — XAI / Interpretability**
- **Concept B — Clinical / Medical Context**

Two structural differences from the PubMed string, both **deliberate broadenings** that should be watched for precision drift when this is run live:

1. **Field tag is `:ti,ab,kw` (title, abstract, *and* author keywords), not just title/abstract.** Embase has no exact equivalent of PubMed's `[tiab]`; `:ti,ab` is the closest match, but `:ti,ab,kw` is the conventional systematic-review default because Embase indexing relies more heavily on author keywords than MEDLINE does. This will likely retrieve a modestly larger set than a strict title/abstract-only translation — note this if the hit count comes back surprisingly high relative to PubMed's 9,672.
2. **Emtree controlled-vocabulary candidates are offered for the 5 MeSH terms in Concept B**, but are marked "to verify" rather than included by default (see Concept B section). Given the PubMed v1 lesson — that adding generic vocabulary (e.g., "black box," "feature importance") inflated Concept A from 9,672 to 15,385+ hits without adding confirmed recall — do not add broad Emtree explosions (e.g., `'machine learning'/exp`, `'artificial intelligence'/exp`) to Concept A. They would very likely repeat that over-broadening, this time at Embase scale (Embase indexes more conference proceedings and is generally larger than MEDLINE for non-English/grey literature too).

**Recall validation status:** Both MEDLINE-indexed benchmark papers from the PubMed validation (PMID 37543055 — Cao, Kunaprayoon & Ren 2023; PMID 32541594 — Tosun et al. 2020) are also indexed in Embase (Embase indexes MEDLINE content). These two are the recommended retrievability test cases for this string — confirm both appear in the Embase result set before trusting the hit count.

---

## Concept A — XAI / Interpretability (DRAFT)

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

**Translation notes:**
- Double quotes → single quotes (`'...'`), the Embase.com phrase-search convention.
- `[tiab]` → `:ti,ab,kw` (see Design Rationale point 1).
- Truncation symbol `*` is unchanged — Embase.com uses the same `*` wildcard as PubMed for "zero or more characters." (If your institution uses **Ovid Embase** instead of Embase.com, truncation is `$` or `*` depending on configuration — verify which your platform uses before pasting.)
- **Emtree candidate (optional, NOT included above — verify before adding):** `'explainable artificial intelligence'/exp` — Emtree added this as a term in recent years. If it exists and is reasonably scoped (not auto-exploding into generic "artificial intelligence"), it could supplement the free-text block. Check via Embase's "Map Term"/Emtree thesaurus browser. **Do not add `'machine learning'/exp` or `'artificial intelligence'/exp`** — these would almost certainly reproduce the over-broadening diagnosed in PubMed v1 rev 3 (70,946 hits for Concept A alone with generic terms included).

---

## Concept B — Clinical / Medical Context (DRAFT)

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

**MeSH → Emtree mapping table (all 5 candidates below MUST be verified via Embase's Map Term/Emtree thesaurus browser before this string is run for the record — Emtree preferred-term labels frequently differ from MeSH in wording, and `/exp` explosion scope can differ substantially):**

| PubMed MeSH term | Emtree candidate (UNVERIFIED) | Notes |
|---|---|---|
| "Decision Support Systems, Clinical"[Mesh] | `'clinical decision support system'/exp` | Likely a direct match — Emtree has an equivalent term, but confirm singular/plural and exact label |
| "Physicians"[Mesh] | `'doctor'/exp` | Emtree's preferred term for this concept is historically "doctor," not "physician" — MeSH "Physicians" maps to Emtree "doctor" in most Elsevier crosswalks, but verify |
| "Clinical Decision-Making"[Mesh] | `'decision making'/exp` | Emtree may not have a "clinical" qualifier on this term — `/exp` on the broader "decision making" could be too broad (risk of re-introducing precision loss); consider testing without this term first |
| "Diagnosis, Computer-Assisted"[Mesh] | `'computer assisted diagnosis'/exp` | Likely a direct match, but confirm hyphenation/spacing in Emtree's actual label |
| "Patient Care"[Mesh] | `'patient care'/exp` | Likely a direct match |

**If live testing shows the Emtree terms (especially `'decision making'/exp`) are adding large numbers of hits without improving recall on the two benchmark papers, drop them and rely on the free-text `:ti,ab,kw` block alone** — this mirrors the precision-tuning logic from PubMed v1 rev 3.

---

## Full Combined String (DRAFT — paste into Embase.com search box for first live test)

```
(Concept A) AND (Concept B) AND [2015-2024]/py AND [english]/lim
```

```
('explainable artificial intelligence':ti,ab,kw OR 'explainable AI':ti,ab,kw OR 'XAI':ti,ab,kw OR 'interpretable machine learning':ti,ab,kw OR 'interpretability':ti,ab,kw OR 'model interpretability':ti,ab,kw OR 'explainability':ti,ab,kw OR 'explainable model*':ti,ab,kw OR 'SHAP':ti,ab,kw OR 'Shapley additive explanation*':ti,ab,kw OR 'Shapley value*':ti,ab,kw OR 'LIME':ti,ab,kw OR 'local interpretable model-agnostic':ti,ab,kw OR 'Grad-CAM':ti,ab,kw OR 'gradient-weighted class activation':ti,ab,kw OR 'class activation map*':ti,ab,kw OR 'counterfactual explanation*':ti,ab,kw OR 'feature attribution':ti,ab,kw OR 'rule extraction':ti,ab,kw OR 'prototype-based explanation':ti,ab,kw OR 'prototype explanation*':ti,ab,kw OR 'case-based explanation*':ti,ab,kw OR 'interpretable AI':ti,ab,kw OR 'interpretable artificial intelligence':ti,ab,kw OR 'explainable deep learning':ti,ab,kw)
AND
('clinical decision support':ti,ab,kw OR 'clinical decision support system*':ti,ab,kw OR 'CDSS':ti,ab,kw OR 'computer-aided diagnos*':ti,ab,kw OR 'computer aided diagnos*':ti,ab,kw OR 'diagnostic algorithm*':ti,ab,kw OR 'predictive model*':ti,ab,kw OR 'risk prediction model*':ti,ab,kw OR 'clinical':ti,ab,kw OR 'clinician*':ti,ab,kw OR 'physician*':ti,ab,kw OR 'radiolog*':ti,ab,kw OR 'patholog*':ti,ab,kw OR 'nurse*':ti,ab,kw OR 'diagnosis':ti,ab,kw OR 'diagnostic':ti,ab,kw OR 'prognosis':ti,ab,kw OR 'treatment':ti,ab,kw OR 'patient care':ti,ab,kw OR 'hospital*':ti,ab,kw OR 'clinical decision support system'/exp OR 'doctor'/exp OR 'decision making'/exp OR 'computer assisted diagnosis'/exp OR 'patient care'/exp)
AND [2015-2024]/py
AND [english]/lim
```

**Date/language syntax caveat — read before running:** `[2015-2024]/py` (publication year) and `[english]/lim` (language limit) are the standard Embase.com inline-query syntax forms, but Embase.com's search interface also offers an equivalent **"Limits" sidebar** (Date of Publication range, Language checkboxes) applied *after* the query runs — analogous to PubMed's filter sidebar. **This is exactly the mechanism that produced the 36-hit false result in the PubMed run** (extra filters — Review/Systematic Review/Aged 65+ — were silently stacked alongside Date+Language). Before recording any Embase hit count:
1. Check the Limits/sidebar panel and confirm **only** Date of Publication (2015–2024) and Language (English) are active — no document-type, subject, or age-group filters.
2. If the inline `/py` and `/lim` syntax above causes a syntax error, remove those two clauses from the query and apply Date + Language via the sidebar instead, then re-verify the sidebar state per step 1.

---

## Known Limitations / Things to Verify Live

1. **Platform ambiguity (Embase.com vs. Ovid Embase):** This draft assumes Embase.com syntax (`'term':ti,ab,kw`, `'term'/exp`, `[2015-2024]/py`). If your institutional access is via **Ovid** (the same interface used for Ovid MEDLINE), the syntax differs: field tags become `.ti,ab,kf.`, explosion is `exp` as a prefix keyword (`exp Decision Support Systems, Clinical/`), truncation is `$` (Ovid's default) or `*`, and date/language are `.yr.` and `limit to english language`. **Determine which platform your institution provides before the first live run** — this changes nearly every line of this document.
2. **Emtree term existence and scope are entirely unverified** (see MeSH→Emtree table above) — this is the single biggest source of uncertainty in this draft.
3. **`:ti,ab,kw` vs. `:ti,ab`** — if the hit count is dramatically higher than PubMed's 9,672 (e.g., >20,000), consider testing `:ti,ab` (drop author keywords) as a precision check, analogous to the PubMed Concept-A-alone diagnostic.
4. **Embase indexes conference proceedings and abstracts more heavily than MEDLINE** — expect a higher proportion of conference-abstract-only records (no full text), which may need a publication-type filter at the screening stage (not the search stage) to flag for the full-text screening criteria (`screening_fulltext_criteria.md`, E4 — wrong publication type).
5. **No new test cases beyond the 2 MEDLINE-indexed benchmark papers** — Embase doesn't add new retrievability test cases beyond what PubMed already validated, since Embase is a superset that includes MEDLINE content. (ACM-published benchmark papers — Kumar et al., Gu et al. — are very unlikely to be in Embase, which is biomedical-focused; do not expect them here.)

---

## Next Steps

1. Confirm Embase.com vs. Ovid Embase platform for institutional access.
2. Run the Full Combined String (or its Ovid equivalent) live; record the raw hit count here and in `data/screening/prisma_counts.csv` (row "Records from database: Embase").
3. Verify both benchmark papers (PMID 37543055, PMID 32541594) appear in the result set.
4. Resolve the 5 Emtree candidates via Map Term/thesaurus browser; update the MeSH→Emtree table with confirmed labels and re-run if any candidate is missing or substantially changes the count.
5. If hit count is wildly out of proportion to PubMed's 9,672 (either direction), apply the precision-tuning checks in point 3 above before logging a final count.
6. Once stable, log the final string, hit count, and any deviations from this draft in `memos/decision_log.md`.

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1 draft (UNTESTED) | 2026-06-09 | Initial field-syntax translation from PubMed v1 rev 3 (9,672 hits). Concept A and B free-text terms converted to `:ti,ab,kw`; 5 MeSH terms mapped to unverified Emtree candidates. Not yet run live. |
