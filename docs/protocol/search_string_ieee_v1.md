# IEEE Xplore Search String v1 — Clinical XAI Systematic Review (9970)

**Issue:** #22
**Status:** DRAFT / UNTESTED — translated from the validated PubMed v1 rev 3 string (`search_string_pubmed_v1.md`, 9,672 hits). Not yet run against live IEEE Xplore. Hit counts, field-tag-group syntax, and year-range filter behaviour all require live verification.
**Database:** IEEE Xplore Digital Library (Command Search)
**Date range filter (target):** 2015–2024
**Language filter (target):** English (no separate language field in IEEE Xplore — see Known Limitations)

---

## Design Rationale

This is a field-syntax translation of the finalized PubMed v1 rev 3 string (see `search_string_pubmed_v1.md` for the full diagnostic history: 9 → 36 → 15,385 → 9,672 hits). The two-concept AND structure is preserved:

- **Concept A — XAI / Interpretability**
- **Concept B — Clinical / Medical Context**

Two structural differences from the PubMed string, both **driven by IEEE Xplore having no clinical-domain controlled vocabulary**:

1. **The 5 MeSH terms in Concept B are dropped entirely** — IEEE's "IEEE Terms" thesaurus is engineering/CS-focused (e.g., "Medical diagnostic imaging," "Biomedical imaging") and has no equivalent to MeSH headings like "Clinical Decision-Making" or "Patient Care." Concept B here is free-text-only, same situation as PubMed's Concept A (which also has no controlled-vocabulary backstop — see `search_string_pubmed_v1.md` Known Limitations item 1).
2. **Field scoping requires repeating the field tag per term** (or per OR-group, syntax TBD live) — IEEE Xplore's Command Search has no single field code equivalent to PubMed's `[tiab]`. Two candidate query forms are given below (Option 1: unrestricted baseline; Option 2: field-restricted to Document Title + Abstract + Author Keywords). **Start with Option 1** — it is far less likely to hit a syntax error and gives an immediate upper-bound hit count.

**Recall validation status — IEEE has no confirmed benchmark paper.** Of the four non-MEDLINE benchmark papers identified during PubMed validation (`search_string_pubmed_v1.md` Revision note 3, Finding 2):
- Kumar et al. (2021) and Gu et al. (2020/2023) are published in **ACM** Transactions journals — not IEEE.
- Nayebi et al. (2022) is AMIA Symposium / arXiv — not an IEEE venue.
- Clough et al. (2019) is MICCAI / Springer LNCS / arXiv — not an IEEE venue.

**None of these are usable as IEEE Xplore retrievability test cases.** IEEE Xplore's most relevant venues for clinical XAI are likely **IEEE Transactions on Medical Imaging (TMI)** and **IEEE Journal of Biomedical and Health Informatics (JBHI)** — both publish Grad-CAM/attention/SHAP-based medical-imaging interpretability work. No specific test-case paper is identified yet; **if full-text screening later identifies an included paper published in TMI, JBHI, or another IEEE venue, retroactively confirm this string retrieves it** and log the result.

---

## Concept A — XAI / Interpretability (DRAFT, free-text only)

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

**Translation notes:**
- `[tiab]` quoting is preserved as `"..."` — IEEE Xplore uses double quotes for exact-phrase matching (and to disable stemming).
- Truncation symbol `*` is unchanged — per IEEE's Advanced Search Tips, `*` matches "a single character, multiple characters, or no characters" (functionally equivalent to PubMed's `*`). `?` is also available for exactly one character if a spelling-variant need arises.
- No controlled-vocabulary additions — same free-text-only situation as PubMed Concept A.

---

## Concept B — Clinical / Medical Context (DRAFT, free-text only — MeSH terms dropped)

```
("clinical decision support" OR "clinical decision support system*" OR CDSS
OR "computer-aided diagnos*" OR "computer aided diagnos*"
OR "diagnostic algorithm*" OR "predictive model*" OR "risk prediction model*"
OR clinical OR "clinician*" OR "physician*" OR "radiolog*"
OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic
OR prognosis OR treatment OR "patient care" OR "hospital*")
```

**Translation notes:**
- The 5 MeSH terms (`Decision Support Systems, Clinical`, `Physicians`, `Clinical Decision-Making`, `Diagnosis, Computer-Assisted`, `Patient Care`) are **dropped, not translated** — see Design Rationale point 1. This is expected to make Concept B's contribution to precision weaker than in PubMed/Embase/CINAHL; the free-text terms (especially the broad single-word terms `clinical`, `diagnosis`, `treatment`, `prognosis`) carry the full Concept B load here.
- **Watch for this being the dominant source of any over-broad hit count** — if the IEEE result count is disproportionately large relative to PubMed's 9,672, the broad single-word Concept B terms (`clinical`, `diagnosis`, `diagnostic`, `prognosis`, `treatment`, `hospital*`) combined with IEEE's "Full Text & Metadata" default scope (see Known Limitations) are the most likely cause — not Concept A.

---

## Full Combined String — Option 1 (RECOMMENDED FIRST TEST: unrestricted Command Search)

```
(Concept A) AND (Concept B)
```

```
("explainable artificial intelligence" OR "explainable AI" OR XAI OR "interpretable machine learning" OR interpretability OR "model interpretability" OR explainability OR "explainable model*" OR SHAP OR "Shapley additive explanation*" OR "Shapley value*" OR LIME OR "local interpretable model-agnostic" OR "Grad-CAM" OR "gradient-weighted class activation" OR "class activation map*" OR "counterfactual explanation*" OR "feature attribution" OR "rule extraction" OR "prototype-based explanation" OR "prototype explanation*" OR "case-based explanation*" OR "interpretable AI" OR "interpretable artificial intelligence" OR "explainable deep learning")
AND
("clinical decision support" OR "clinical decision support system*" OR CDSS OR "computer-aided diagnos*" OR "computer aided diagnos*" OR "diagnostic algorithm*" OR "predictive model*" OR "risk prediction model*" OR clinical OR "clinician*" OR "physician*" OR "radiolog*" OR "patholog*" OR "nurse*" OR diagnosis OR diagnostic OR prognosis OR treatment OR "patient care" OR "hospital*")
```

Paste this directly into the **Command Search** box (not the basic search box) at ieeexplore.ieee.org. With no field tags, IEEE Xplore searches **"Full Text & Metadata"** by default — **this is much broader than PubMed's `[tiab]`** (it includes the full body text of every paper, references, etc.). Expect a substantially higher hit count than 9,672. Treat this as an **upper-bound baseline**, not a final count.

---

## Full Combined String — Option 2 (precision-restricted: Document Title + Abstract + Author Keywords)

```
(("Document Title":(Concept A) OR "Abstract":(Concept A) OR "Author Keywords":(Concept A)))
AND
(("Document Title":(Concept B) OR "Abstract":(Concept B) OR "Author Keywords":(Concept B)))
```

where `(Concept A)` and `(Concept B)` are the two parenthesized OR-blocks defined above, substituted in place of each placeholder (i.e., this expands to three copies of the Concept A block and three copies of the Concept B block, one per field tag).

**This syntax is UNVERIFIED — IEEE's Command Search documentation gives single-term field-tag examples (e.g., `"Document Title":deep learning`) but does not confirm whether a field tag can scope an entire parenthesized OR-group.** Test with a small fragment first, e.g.:

```
"Document Title":(XAI OR "explainable AI")
```

- **If this returns sensible results** (i.e., it behaves as `"Document Title":XAI OR "Document Title":"explainable AI"`, not as a literal phrase search for the whole group), the full Option 2 string can be built by substitution as described.
- **If it errors or behaves unexpectedly**, fall back to repeating the field tag before every individual term — i.e., `"Document Title":XAI OR "Document Title":"explainable AI" OR "Document Title":"interpretable machine learning" OR ...` for all ~24 Concept A terms × 3 fields, and ~20 Concept B terms × 3 fields. This is mechanical but extremely verbose (roughly 130 field-tagged clauses total) — consider doing this with a find-and-replace script on the Concept A/B term lists above rather than by hand.

---

## Known Limitations / Things to Verify Live

1. **No language filter field** — IEEE Xplore does not have a dedicated "Language" search field or limiter the way PubMed/Embase/CINAHL do (the vast majority of IEEE content is English-language by default). If non-English results appear and need excluding, this will likely need to happen at the screening stage rather than the search stage — note this as a deviation from the other three databases' search-stage language filter.
2. **Year range filter is UI/sidebar-based** — IEEE Xplore's "Filters" sidebar has a "Year" facet (checkboxes or range). Apply 2015–2024 there after running the query. **Same filter-stacking caution as the PubMed 36-hit incident**: confirm no other facets (Content Type, Publisher, etc.) are inadvertently applied — in particular, do NOT filter Content Type to "Journals" only unless that is a deliberate decision, since relevant work may appear in IEEE conference proceedings (e.g., EMBC, BIBM).
3. **Option 1's "Full Text & Metadata" default scope is a major precision risk** — full-text search means a paper that merely *cites* an XAI paper, or *cites* a clinical paper, in its references could match both Concept A and Concept B without either concept being central to the paper itself. If Option 1's hit count is enormous (e.g., tens of thousands), Option 2 (metadata-field-restricted) is likely necessary for a workable screening set, despite its syntax complexity.
4. **Option 2's field-tag-group syntax is unverified** (see above) — this is the single biggest open question for this database.
5. **No controlled vocabulary for either concept** — both Concept A and Concept B rely entirely on free-text matching, making this string the most precision-fragile of the four database translations. Expect to iterate on this one the most during live testing.

---

## Next Steps

1. Run **Option 1** (unrestricted Command Search) live; record the raw hit count as a baseline.
2. Test the small Option 2 fragment (`"Document Title":(XAI OR "explainable AI")`) to determine whether field-tag-group syntax works.
3. Based on step 2's result, either build the full Option 2 string by substitution, or construct the per-term-repeated fallback (consider scripting this).
4. Apply the Year (2015–2024) filter via the sidebar, confirming no other facets are stacked.
5. Record the final hit count here and in `data/screening/prisma_counts.csv` (row "Records from database: IEEE Xplore").
6. Once stable, log the final string, hit count, and the chosen Option (1 vs. 2) in `memos/decision_log.md`.
7. Flag for the manuscript: no IEEE-specific retrievability benchmark exists yet — retroactively validate against any IEEE-published paper that survives full-text screening.

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1 draft (UNTESTED) | 2026-06-09 | Initial translation from PubMed v1 rev 3 (9,672 hits). 5 MeSH terms dropped (no IEEE equivalent); two candidate query forms provided (Option 1: unrestricted baseline; Option 2: field-restricted, syntax unverified). Not yet run live. |
