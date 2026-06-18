# PubMed Search String — Clinical XAI Review (9970)

**Issue:** #15 (cross-domain v1); extended under Issue #22 / 2026-06-10 EM pivot (Concept C)
**Status:** v1 rev 3 (cross-domain, 9,672 hits) is **SUPERSEDED** by the 2026-06-10 pivot back to the original EM/ED-only proposal scope (`memos/decision_log.md`). A new Concept C (Emergency Department / triage / ESI / acuity / disposition terms) has been added and ANDed against Concepts A and B. **Final v2 string: A+B+C, date range extended to "present"** (decision recorded 2026-06-10 — see Date Range Decision below). Live-verified via E-utilities on 2026-06-10: **213 hits** (A+B+C, 2015/01/01–2024/12/31) and **497 hits** (A+B+C, 2015/01/01–2026/06/10). Cross-domain v1 rev 3 retained below for audit trail. EM-narrowed v2 string design is FINALIZED, **recall-benchmarked (2026-06-11, 6/8 = 75% — see EM-Specific Recall Benchmark below)**, and **formally executed for PubMed (2026-06-10, 497 records, raw export `data/searches/pubmed-explainabl-set.nbib`)**. Embase/IEEE Xplore/ACM Digital Library executions remain pending (Next Steps item 10).
**Database:** MEDLINE via PubMed
**Date range filter:** 2015/01/01 – search execution date (rolling; live-verified through 2026/06/10 = 497 hits, see Date Range Decision)
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

## Concept C — Emergency Department / Triage Context (NEW — EM Pivot, 2026-06-10)

Added per the 2026-06-10 pivot back to the original proposal scope (`memos/decision_log.md`): an Emergency-Medicine-only scoping review restricted to decisions made during the initial ED encounter (intake, ESI/acuity scoring, immediate disposition — see `docs/protocol/inclusion_boundary.md` v2).

```
("emergency department"[tiab] OR "emergency room"[tiab] OR "emergency medicine"[tiab]
OR "emergency severity index"[tiab] OR "ESI"[tiab]
OR "Triage"[tiab]
OR "acuity scor*"[tiab] OR "acuity assessment"[tiab] OR "acuity level*"[tiab] OR "acuity classification"[tiab]
OR "disposition decision*"[tiab] OR "ED disposition"[tiab] OR "discharge disposition"[tiab]
OR "patient intake"[tiab]
OR "Emergency Service, Hospital"[Mesh] OR "Triage"[Mesh])
```

**Design rationale:** Terms map directly onto Gate 1 of `inclusion_boundary.md` v2 (intake / acuity-ESI / immediate disposition), plus the two MeSH terms that index the ED setting and the triage process directly. `"ESI"[tiab]` is included as a bare 3-letter acronym alongside the spelled-out `"emergency severity index"[tiab]` — ambiguous in isolation (could collide with "electrospray ionization" etc.), but within an AND against Concept A's XAI vocabulary, cross-contamination risk is negligible, and any false positives are caught cheaply at title/abstract screening given the EM-narrowed corpus is small (213–234 records, see below). Other national acuity-scale names (CTAS, MTS, ATS) are deliberately **not** added as separate terms — `inclusion_boundary.md` treats them as in-scope under "acuity scoring" at the screening stage; flagged as a residual watch item below.

**The EMS / inpatient / ICU exclusions in `inclusion_boundary.md` Gate 1 are deliberately NOT encoded as search-string NOT clauses.** Same sensitivity-favouring logic as the original Concept A/B design (see `Design Rationale` above): a paper studying an inpatient deterioration model might still mention "emergency department" in its background section, and a NOT clause risks excluding genuinely in-scope ED-disposition papers that happen to also discuss inpatient or ICU contexts elsewhere. The decision-point-vs-population-origin distinction is a screening-stage judgment (`inclusion_boundary.md` Gate 1 operational note), not a search-string filter.

**Diagnostic finding — phrase-index drop (2026-06-10):** Testing the EM-narrowed query via PubMed E-utilities (esearch JSON) surfaced a `quotedphrasesnotfound` warning for `"prototype-based explanation"[tiab]` and `"prototype explanation*"[tiab]` — both silently dropped from the executed query; only `"case-based explanation*"[tiab]` (normalized to `"case based explanation*"[Title/Abstract]`) was retained. Revision note 2 (above) had reported these forms as "passing indexing" based on PubMed UI testing; this E-utilities run shows two of the three are in fact dropped. **This affects the existing cross-domain v1 rev 3 string identically** (same Concept A block) — it is not a defect introduced by Concept C, and the 9,672 cross-domain count already reflects this silent drop. Logged as a residual watch item for both strings (see Known Limitations item 6); not blocking for the EM pivot given the EM-narrowed corpus is small enough for a dedicated recall benchmark to check directly for prototype/case-based-explanation papers.

---

## Date Range Decision (2026-06-10)

The original proposal's date range (2015/01/01–2024/12/31) was set when the cross-domain v1 string was finalized (2026-06-07). At that time no EM-narrowed search had yet been run, and the preregistration draft (Section 10) planned a separate "January 2025 onward" search update for Phase 3, shortly before manuscript submission.

**Live E-utilities check (2026-06-10) of the A+B+C string, year by year:**

| Period | Hits |
|---|---|
| 2020 | 12 |
| 2021 | 28 |
| 2022 | 45 |
| 2023 | 50 |
| 2024 | 78 |
| 2025 | 139 |
| 2026 (Jan 1 – Jun 10, partial year) | 171 |
| **2015–2024 total** | **213** |
| **2015–2026/06/10 total** | **497** |

**Finding:** the EM+XAI literature is growing exponentially (roughly doubling year-over-year since 2022). The 18 months from January 2025 to June 2026 alone contain **284 records — more than the entire 2015–2024 corpus (213)**. Spot-checking a sample of 2026-dated records (PMIDs 42266581, 42260815, 42257858) confirms these are genuinely recent publications (epub/pubdate May–June 2026), not forward-dated "ahead of print" artifacts.

**Decision: extend the date range to "2015/01/01 through the search execution date", executed as a single search now, rather than deferring 2025+ to a separate Phase 3 update.** Deferring the bulk of the most recent — and, given RQ3's regulatory-readiness framing, arguably most relevant — literature to a lighter later pass would be methodologically inconsistent with how the 2015–2024 corpus is screened. A corpus of ~497 records (as of 2026-06-10) remains within the scope of single-reviewer T/A screening (`docs/protocol/screening_criteria.md`).

**Implication for Phase 3:** the previously-planned "January 2025 onward search update" becomes a much smaller top-up search — only records published/indexed between this search's execution date and shortly before manuscript submission — consistent with standard PRISMA-ScR practice of re-running searches close to submission.

**Note:** the 497-hit figure was a 2026-06-10 snapshot for design purposes. **Confirmed via formal execution (2026-06-10):** the executed A+B+C search (date range upper bound = 2026/06/10) returned exactly **497 records**, matching the snapshot — see `data/searches/pubmed-explainabl-set.nbib` and `data/screening/prisma_counts.csv`.

---

## Full Combined String — Cross-Domain v1 rev 3 (SUPERSEDED 2026-06-10 — retained for audit trail; see EM-Narrowed string below for current scope)

```
(Concept A) AND (Concept B)

AND ("2015/01/01"[Date - Publication] : "2024/12/31"[Date - Publication])
AND English[Language]
```

Paste-ready single-line version (PubMed search box) — validated, 9,672 hits, cross-domain (**SUPERSEDED — see EM-Narrowed string below**):

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

## Full Combined String — EM-Narrowed (v2 FINAL, 2026-06-10 — current scope)

**FINAL: (Concept A) AND (Concept B) AND (Concept C) AND (date) AND (language) — A+B+C, 213 hits (2015–2024) / 497 hits (2015–2026/06/10, live-verified):**

Replace `<SEARCH-EXECUTION-DATE>` with the actual date the search is run. **Executed for PubMed on 2026-06-10** with `<SEARCH-EXECUTION-DATE>` = `2026/06/10` — 497 hits, raw export `data/searches/pubmed-explainabl-set.nbib` (matches the live-verified design-time snapshot exactly). The `<SEARCH-EXECUTION-DATE>` placeholder remains in the string below for the three remaining database translations (Embase, IEEE Xplore, ACM Digital Library — Next Steps item 10), which should use the same 2026/06/10 upper bound for consistency ("execute all four database searches on the same date").

```
("explainable artificial intelligence"[tiab] OR "explainable AI"[tiab] OR "XAI"[tiab] OR "interpretable machine learning"[tiab] OR "interpretability"[tiab] OR "model interpretability"[tiab] OR "explainability"[tiab] OR "explainable model*"[tiab] OR "SHAP"[tiab] OR "Shapley additive explanation*"[tiab] OR "Shapley value*"[tiab] OR "LIME"[tiab] OR "local interpretable model-agnostic"[tiab] OR "Grad-CAM"[tiab] OR "gradient-weighted class activation"[tiab] OR "class activation map*"[tiab] OR "counterfactual explanation*"[tiab] OR "feature attribution"[tiab] OR "rule extraction"[tiab] OR "prototype-based explanation"[tiab] OR "prototype explanation*"[tiab] OR "case-based explanation*"[tiab] OR "interpretable AI"[tiab] OR "interpretable artificial intelligence"[tiab] OR "explainable deep learning"[tiab])
AND
("clinical decision support"[tiab] OR "clinical decision support system*"[tiab] OR "CDSS"[tiab] OR "computer-aided diagnos*"[tiab] OR "computer aided diagnos*"[tiab] OR "diagnostic algorithm*"[tiab] OR "predictive model*"[tiab] OR "risk prediction model*"[tiab] OR "clinical"[tiab] OR "clinician*"[tiab] OR "physician*"[tiab] OR "radiolog*"[tiab] OR "patholog*"[tiab] OR "nurse*"[tiab] OR "diagnosis"[tiab] OR "diagnostic"[tiab] OR "prognosis"[tiab] OR "treatment"[tiab] OR "patient care"[tiab] OR "hospital*"[tiab] OR "Decision Support Systems, Clinical"[Mesh] OR "Physicians"[Mesh] OR "Clinical Decision-Making"[Mesh] OR "Diagnosis, Computer-Assisted"[Mesh] OR "Patient Care"[Mesh])
AND
("emergency department"[tiab] OR "emergency room"[tiab] OR "emergency medicine"[tiab] OR "emergency severity index"[tiab] OR "ESI"[tiab] OR "Triage"[tiab] OR "acuity scor*"[tiab] OR "acuity assessment"[tiab] OR "acuity level*"[tiab] OR "acuity classification"[tiab] OR "disposition decision*"[tiab] OR "ED disposition"[tiab] OR "discharge disposition"[tiab] OR "patient intake"[tiab] OR "Emergency Service, Hospital"[Mesh] OR "Triage"[Mesh])
AND ("2015/01/01"[Date - Publication] : "<SEARCH-EXECUTION-DATE>"[Date - Publication])
AND English[Language]
```

**Decision (2026-06-10): A+B+C is the final v2 structure** (per `memos/decision_log.md`). Concept B is retained for consistency with the cross-domain design's validated two-concept structure (Concept A AND Concept B already underwent the precision-tuning and recall validation documented in Revision note 3) and as an additional layer of clinical-context specificity. The ~9% reduction relative to A+C (213 vs. 234 at the 2015–2024 window) is an acceptable trade-off: any Gate-1-relevant record dropped by Concept B but caught by a broader A+C search would, per the T/A-stage sensitivity-favouring rule (`docs/protocol/screening_criteria.md` Section 3), need to clearly fail a gate to be excluded — Concept B's terms (`clinical`, `diagnosis`, `treatment`, `patient care`, etc.) are broad enough that a genuinely in-scope ED/XAI paper failing to match any of them in title/abstract is unlikely.

**Rejected alternative — (Concept A) AND (Concept C) AND (date) AND (language) — A+C, 234 hits (2015–2024):**

```
("explainable artificial intelligence"[tiab] OR "explainable AI"[tiab] OR "XAI"[tiab] OR "interpretable machine learning"[tiab] OR "interpretability"[tiab] OR "model interpretability"[tiab] OR "explainability"[tiab] OR "explainable model*"[tiab] OR "SHAP"[tiab] OR "Shapley additive explanation*"[tiab] OR "Shapley value*"[tiab] OR "LIME"[tiab] OR "local interpretable model-agnostic"[tiab] OR "Grad-CAM"[tiab] OR "gradient-weighted class activation"[tiab] OR "class activation map*"[tiab] OR "counterfactual explanation*"[tiab] OR "feature attribution"[tiab] OR "rule extraction"[tiab] OR "prototype-based explanation"[tiab] OR "prototype explanation*"[tiab] OR "case-based explanation*"[tiab] OR "interpretable AI"[tiab] OR "interpretable artificial intelligence"[tiab] OR "explainable deep learning"[tiab])
AND
("emergency department"[tiab] OR "emergency room"[tiab] OR "emergency medicine"[tiab] OR "emergency severity index"[tiab] OR "ESI"[tiab] OR "Triage"[tiab] OR "acuity scor*"[tiab] OR "acuity assessment"[tiab] OR "acuity level*"[tiab] OR "acuity classification"[tiab] OR "disposition decision*"[tiab] OR "ED disposition"[tiab] OR "discharge disposition"[tiab] OR "patient intake"[tiab] OR "Emergency Service, Hospital"[Mesh] OR "Triage"[Mesh])
AND ("2015/01/01"[Date - Publication] : "2024/12/31"[Date - Publication])
AND English[Language]
```

**Spot-check (top 15 of 234, A+C, 2026-06-10):** Titles span genuinely ED/triage-relevant ML+XAI papers — e.g. "Leveraging machine learning and rule extraction for enhanced transparency in emergency department length of stay prediction"; "Deep learning-based Emergency Department In-hospital Cardiac Arrest Score (Deep EDICAS)..."; "Machine learning outperforms the Canadian Triage and Acuity Scale (CTAS)..."; "Improving triage performance in emergency departments using machine learning and natural language processing: a systematic review" — alongside several expected to fail Gate 1 at screening (inpatient rehabilitation discharge destination, palliative-care timing, post-stroke epilepsy prediction). This is the expected mix for a sensitivity-favouring search awaiting gate-based screening. **A+B+C (213) is a strict subset of A+C (234)** — every A+B+C hit also satisfies A+C — so this spot-check remains qualitatively representative of the final A+B+C string; the 21 records in A+C but not A+B+C are the ones lacking any Concept B term in title/abstract.

**For context — Concept C alone (no XAI requirement), date+language only: 151,954 hits.** Confirms Concept C terms are individually broad (as expected — "emergency department" and "triage" are common terms), and that essentially all of the precision in the EM-narrowed string comes from the AND with Concept A, mirroring the original two-concept design philosophy.

---

## EM-Specific Recall Benchmark (2026-06-11)

Per Next Steps item 9, an EM-specific recall benchmark was assembled and validated against the live A+B+C result set (497 PMIDs, 2015/01/01–2026/06/11 — confirmed stable from the 2026-06-10 snapshot). The cross-domain benchmark in Revision note 3 (Cao/Kunaprayoon/Ren, Tosun, Kumar, Gu) does not transfer to the EM-narrowed scope (none of the four pass `inclusion_boundary.md` v2 Gate 1), so a new benchmark was required.

**Methodology:** `references/bib/foundational.bib` was checked first and ruled out (general XAI-theory papers only, no EM-specific seeds). Candidates were instead identified via an independent PubMed query — deliberately using a *broader, looser* term set than Concept A (including bare `"feature importance"[tiab]`, `"explainable"[tiab]`, `"interpretable"[tiab]` without phrase restrictions) AND an EM/triage/disposition term set, English-language only:

```
("SHAP"[tiab] OR "LIME"[tiab] OR "explainable"[tiab] OR "interpretable"[tiab] OR "explainability"[tiab] OR "feature importance"[tiab] OR "Grad-CAM"[tiab] OR "interpretability"[tiab])
AND ("emergency department"[tiab] OR "emergency severity index"[tiab] OR "ED triage"[tiab] OR "triage"[tiab] OR "disposition"[tiab])
AND English[Language]
```

This returned 653 hits. The top 30 (by relevance) were screened by title/abstract for clinical-XAI relevance to the EM/ED setting; 8 candidates were retained and checked for membership in the live A+B+C idlist, then diagnosed per-concept (A/B/C tested individually AND'd with `[uid]`) where retrieval was a miss or otherwise informative.

**Results (abstract-level Gate assessments — full text not reviewed):**

| # | PMID | Title (short) | Year | Retrieved by A+B+C? | Gate 1 | Gate 2 | Gate 3 | Notes |
|---|---|---|---|---|---|---|---|---|
| 1 | 38708185 | SERP+: improved interpretable ML ED triage tool (class imbalance) | 2024 | ✓ | Pass — acuity/mortality-risk triage scoring | Likely pass — AutoScore-Imbalance produces an inherently interpretable point-based score, framed as "interpretable" in the title | Uncertain — reports predictive-performance metrics (AUC/sensitivity/specificity); no explicit evaluation of the score's interpretability in the abstract | Retrieved via `"interpretable machine learning"[tiab]` |
| 2 | 38102476 | RISKINDEX: explainable ML for ED risk stratification (multicenter) | 2024 | ✓ | Pass — risk stratification at ED triage | Pass — SHAP explicitly applied | Uncertain — SHAP "used to visualize" predictions; no explicit fidelity/clinician evaluation of the explanations described in the abstract | Retrieved via `"SHAP"[tiab]` |
| 3 | 39176941 | AI models for medium-risk ED disposition outcome | 2024 | **✗ NOT RETRIEVED** | Pass — disposition outcome (admit/discharge) | Borderline — "feature importance" used for feature *selection*, not framed as an explanation method | Likely fail — no evaluation of feature importance as an explanation | Concept A = 0 — "feature importance" ≠ "feature attribution"; even if retrieved, plausibly excluded at Gate 2/3 anyway |
| 4 | 40242564 | Interpretable ML for CT-abnormality prediction in mTBI | 2025 | ✓ | **Fail** — decision is whether to order a CT scan, not intake/acuity/disposition | Pass — SHAP explicitly applied and discussed | n/a (Gate 1 fail) | Retrieved correctly (`"interpretable machine learning"[tiab]`/`"SHAP"[tiab]`); excluded at Gate 1 — search casts a wider net than the inclusion boundary, as designed |
| 5 | 37578440 | ED-triage-based ML for admission/mortality prediction (permutation feature importance) | 2023 | **✗ NOT RETRIEVED** | Pass — admission/disposition + mortality prediction at ED triage | Borderline-pass — "permutation feature importance" is a recognized model-agnostic feature-attribution method | Uncertain — importance rankings reported as results; explicit evaluation of the explanation unclear from the abstract | Concept A = 0 — same gap as #3, but the more plausible Gate-2 pass; **the more concerning of the two misses** |
| 6 | 36634916 | Early prediction of hospital admission of ED patients | 2023 | ✓ | Pass — admission prediction at multiple post-arrival timepoints | Uncertain — "SHAP" appears only as an author keyword (MEDLINE "Other Term"/OT field), not in the visible title/abstract; full text needed | Uncertain | Retrieved via `"SHAP"[tiab]` matching the OT field — confirms PubMed's `[tiab]`/"Title/Abstract" search extends to author keywords, a recall **strength** |
| 7 | 39176843 | ED length-of-stay classification with rule extraction | 2024 | ✓ | **Fail** — LOS is an operational/throughput metric, not intake/acuity/disposition | Pass — explicit rule extraction | n/a (Gate 1 fail) | Retrieved correctly via `"rule extraction"[tiab]`; excluded at Gate 1 — same "wider net" pattern as #4 |
| 8 | 40102847 | Interpretable ML for ED wait-time prediction | 2025 | ✓ | **Fail** — wait time is an operational/throughput metric | Pass — SHAP + "interpretable" | n/a (Gate 1 fail) | Retrieved correctly via `"interpretable machine learning"[tiab]`/`"SHAP"[tiab]`; excluded at Gate 1 — same pattern |

**Finding 1 — recall: 6/8 (75%) retrieved.** The two misses (#3, #5) share a single root cause: both use "feature importance" / "permutation feature importance" phrasing, which is **not** in Concept A's term list (only `"feature attribution"[tiab]` is present — see Removed-terms note under Concept A, which dropped a bare `"feature importance"[tiab]` term in Revision note 3 for over-broadening reasons).

**Finding 2 — the gap's severity is limited.** Per-concept diagnosis (Concept A AND Concept B AND Concept C tested individually against `[uid]`) confirmed for both #3 and #5: Concept A = 0, Concept B = 1, Concept C = 1 — i.e., the miss is isolated entirely to Concept A; both papers are clearly EM/ED-context (Concept C) and clinical (Concept B). Of the two: #3 used "feature importance" purely for exploratory feature *selection* with no apparent evaluation of the importances as an explanation — plausibly fails Gate 2/3 even if retrieved. #5 used "permutation feature importance," a recognized model-agnostic feature-attribution technique, and is the more plausible Gate-2 pass — the higher-stakes miss, though it cannot be evaluated further (full text) since it is unretrievable by A+B+C.

**Finding 3 — recall strength confirmed: `[tiab]` indexing includes author keywords.** #6 (36634916) was flagged during the citation-chase as an "unexpected retrieval" — its visible title/abstract contains no Concept A term. Per-term diagnosis found `"SHAP"[tiab]` is the sole match, via the MEDLINE "Other Term" (OT, author-keyword) field (`OT - SHAP`), confirmed by fetching the record in `medline` format. This confirms PubMed's `[tiab]`/"Title/Abstract" search field extends to author-supplied keywords for records that have them — extending recall beyond the literal abstract text, and not previously documented in this protocol.

**Finding 4 — the search string appropriately casts a wider net than the inclusion boundary.** 3/8 candidates (#4, #7, #8) are correctly retrieved by A+B+C (genuine XAI + clinical + ED-context papers) but fail Gate 1 of `inclusion_boundary.md` v2 — #4's decision point is CT-scan-ordering (none of intake/acuity/disposition), and #7/#8 are operational/throughput models (LOS, wait time), explicitly excluded by Gate 1. This is the expected behaviour of a sensitivity-favouring search — screening, not the search string, does this precision work.

**Decision: do not modify the A+B+C term list.** The string was finalized as FINAL (`memos/decision_log.md`, 2026-06-10) with a live-verified hit count (213/497). Adding a bare `"feature importance"[tiab]` term to Concept A would risk reproducing the over-broadening Revision note 3 specifically removed it to avoid (Known Limitations item 2) — "feature importance" is reported in the large majority of tabular-ML papers regardless of any XAI framing. The "feature importance"/"permutation feature importance" gap is instead documented as Known Limitations item 8 below. **Mitigation:** during full-text screening, forward/backward citation-chase any included papers that discuss feature-importance-only explanation methods, recording any additional records found via `data/screening/` "other sources" per `prisma_counts.csv`.

**Conclusion: the A+B+C v2 FINAL string is validated against this EM-specific benchmark** — 6/8 (75%) recall against an independently-assembled candidate set, with both misses attributable to a single, documented, consciously-not-remediated term-list gap, and 3/8 correct-but-Gate-1-excluded retrievals confirming the string's sensitivity-favouring design works as intended for the EM-narrowed scope.

---

## Known Limitations / Residual Watch Items

1. **"ANCHOR" intentionally omitted as a bare term** — too short and ambiguous (matches anatomical anchors, surgical anchors). Coverage relies on "decision rule*"-equivalents being absorbed into "rule extraction"; if a future audit finds ANCHOR-based papers being missed, add `"anchor explanation*"[tiab]` or `"anchors LIME"[tiab]` as a targeted addition.
2. **"Attention," "black box," "saliency map," "feature importance," and "decision rule" were removed (Revision note 3)** — these generic ML/stats terms inflated Concept A from a focused XAI vocabulary to 70,946 hits (vs. ~9,672 for the full combined query), without adding confirmed recall against the independent benchmark. If full-text screening later turns up an included paper that used *only* one of these generic terms (and none of the remaining Concept A vocabulary) in its title/abstract, that would be a genuine miss worth logging — but the benchmark validation found no such case.
3. **MeSH terms lag new technology** — "Artificial Intelligence"[Mesh] and "Machine Learning"[Mesh] may not yet be indexed on very recent papers (indexing lag ~6 months to 2 years). The [tiab] terms compensate for this; do not rely on MeSH alone.
4. **No drug/device brand names included** — by design (Gate 1 excludes drug discovery; consumer wearables are excluded at Gate 1 unless clinically overseen).
5. **Database-coverage gap is now empirically documented (Revision note 3, Finding 2)** — 4 of 6 benchmark candidates that passed the inclusion gates are not indexed in MEDLINE at all (ACM Digital Library, MICCAI proceedings, AMIA/arXiv preprints). This is a structural limitation of PubMed as a single source, not a defect of this string — it is the primary justification for the multi-database translation in Issue #22, and those four papers are now concrete test cases for that translation. **Note:** the original benchmark (Cao/Kunaprayoon/Ren, Tosun, Kumar, Gu) is all non-EM and does not transfer to the EM-narrowed string — a new EM-specific benchmark is needed (see Next Steps).
6. **Prototype-explanation phrase-index drop affects both strings (2026-06-10)** — `"prototype-based explanation"[tiab]` and `"prototype explanation*"[tiab]` are silently dropped by PubMed's phrase index (confirmed via E-utilities `quotedphrasesnotfound`); only `"case-based explanation*"[tiab]` is retained. Affects the cross-domain v1 rev 3 string (9,672) identically — not introduced by Concept C. See the Concept C section above for detail.
7. **National acuity-scale variants (CTAS, MTS, ATS, etc.) not added as separate Concept C terms** — `inclusion_boundary.md` v2 treats these as in-scope under "acuity scoring" at screening, but they are not separately encoded in the search string. If full-text screening turns up a paper using only a non-ESI acuity-scale name (and none of the other Concept C terms) in its title/abstract, that would be a genuine miss worth logging and adding as a targeted term.
8. **"Feature importance" / "permutation feature importance" gap (confirmed 2026-06-11 via the EM-specific recall benchmark)** — Concept A has no bare `"feature importance"[tiab]` term (removed in Revision note 3 for over-broadening reasons; only `"feature attribution"[tiab]` is present). Two of eight EM-specific benchmark candidates (PMID 39176941, 37578440) were missed solely on this basis (Concept A = 0; Concept B and C both = 1). Deliberately not remediated — see EM-Specific Recall Benchmark section above. **Mitigation:** citation-chase from included papers during full-text screening to catch any feature-importance-only-framed papers.

---

## Next Steps

1. ~~Run this string in PubMed; record total hit count here.~~ Done — cross-domain v1 rev 3 returned **9,672 hits** (2015–2024, English) — **SUPERSEDED** by the EM pivot below.
2. ~~Issue #16 — validate recall against seed papers (cross-domain).~~ Done via an independent citation-chased benchmark (see Revision note 3) — both MEDLINE-indexed benchmark papers are retrieved by the cross-domain string. **This benchmark is non-EM and does not validate the EM-narrowed string** (item 7 below).
3. ~~Log the cross-domain string, hit count, and the database-coverage finding in `memos/decision_log.md`~~ Done (2026-06-07/2026-06-09 entries).
4. ~~Translate cross-domain string to other databases (Embase, CINAHL, IEEE Xplore, ACM Digital Library) per Issue #22~~ Done (2026-06-09), but was **superseded** — re-derived with Concept C under item 8.
5. ~~Run each of the four cross-domain draft translations live~~ Superseded — see item 8.
6. ~~Decide A+C vs A+B+C as the v2 EM-narrowed string~~ Done (2026-06-10) — **A+B+C** chosen, retaining Concept B for consistency with the validated cross-domain two-concept design. See decision rationale above and `memos/decision_log.md`.
7. ~~Decide the date range~~ Done (2026-06-10) — extended from a fixed 2015–2024 window to **"2015/01/01 through search-execution date"**, folding the previously-planned Phase 3 "January 2025 onward" update into the initial execution. Live-verified 2026-06-10: 497 hits. See Date Range Decision above and `memos/decision_log.md`.
8. ~~Re-derive Embase/IEEE/ACM translations (Issue #22) by adding Concept C and restructuring to A+B+C with the extended date range~~ Done (2026-06-10) — see `search_string_embase_v1.md`, `search_string_ieee_v1.md`, `search_string_acm_v1.md`. CINAHL translation remains shelved per the EM-pivot database-scope decision.
9. ~~Assemble a new EM-specific recall benchmark (citation-chase from EM/triage XAI papers, or from the proposal's own background reading) and validate the A+B+C string against it~~ Done (2026-06-11) — 8-candidate independent benchmark, 6/8 (75%) retrieved by A+B+C; both misses traced to a single documented term-list gap ("feature importance" vs. "feature attribution"), deliberately not remediated. See EM-Specific Recall Benchmark section above and Known Limitations item 8.
10. Formally execute all four database searches on the same date (raw exports to `data/searches/`), setting the date range's upper bound to that execution date; update `data/screening/prisma_counts.csv`'s Identification rows. **PubMed done (2026-06-10)** — 497 records, `data/searches/pubmed-explainabl-set.nbib`, `prisma_counts.csv` updated. Embase, IEEE Xplore, and ACM Digital Library remain pending — use the same 2026/06/10 date-range upper bound for consistency.
11. Log the final v2 string, hit counts, and this benchmark validation result in `memos/decision_log.md`. **PubMed portion done (2026-06-11 entry, plus the formal-execution addendum below).** Remaining: log once the other three databases are executed.

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1 draft | 2026-06-07 | Initial draft. Two-concept AND structure (XAI terms AND clinical-AI terms). Issue #15. |
| v1 rev 1 | 2026-06-07 | Fixed accidental 3-way AND (removed redundant nested AI/ML tech sub-block from Concept B); 9 hits → corrected structure. |
| v1 rev 2 | 2026-06-07 | Fixed duplicate `AND AND` syntax error and `"prototype-based explanation*"` phrase-index rejection; diagnosed 36-hit result as a filter artifact (Review/Systematic-Review/Aged 65+ filters stacked in PubMed UI), not a string defect. |
| v1 rev 3 | 2026-06-07 | Diagnosed 15,385-hit over-breadth to 5 generic ML/stats term-groups in Concept A (confirmed via Concept-A-alone test: 70,946 hits); removed them, yielding 9,672 hits (37% reduction). Validated recall against an independently citation-chased benchmark (4 papers passing all 3 inclusion gates; 2 indexed in MEDLINE) — both indexed papers retrieved by the final string, confirming zero recall loss. Documented a database-coverage finding (4/6 benchmark candidates not indexed in MEDLINE) that empirically justified the Issue #22 multi-database plan. **SUPERSEDED 2026-06-10 by the EM pivot — retained for audit trail.** |
| v2 — EM pivot (draft) | 2026-06-10 | Added Concept C (Emergency Department / triage / ESI / acuity / disposition terms) per the pivot to the original proposal scope (`memos/decision_log.md`). EM-narrowed string returns **234 hits (A+C, recommended)** or **213 hits (A+B+C)**. Identified a phrase-index drop affecting two prototype-explanation term variants (affects both v1 rev 3 and v2 identically). Pending: A+C vs A+B+C decision, new EM-specific recall benchmark, formal execution/export. |
| v2 — final (A+B+C, date-extended) | 2026-06-10 | **A+B+C** chosen as the final structure (Concept B retained for consistency with the validated cross-domain design). Date range extended from a fixed 2015–2024 window to "2015/01/01 through search-execution date", based on a live E-utilities check showing exponential growth (213 hits 2015–2024 vs. 497 hits 2015–2026/06/10 — the most recent 18 months alone contain more candidate records than the prior decade); folds the planned Phase 3 "January 2025 onward" update into a single initial execution. Embase/IEEE/ACM translations re-derived with Concept C added and restructured to A+B+C (Issue #22). Pending: EM-specific recall benchmark, formal execution/export. |
| v2 — recall-benchmarked | 2026-06-11 | EM-specific recall benchmark completed (Next Steps item 9): 8 independently-identified EM/ED-XAI candidates checked against the live A+B+C idlist (497, 2015–2026/06/11). 6/8 (75%) retrieved; both misses (PMID 39176941, 37578440) traced via per-concept diagnosis to a single Concept A gap ("feature importance"/"permutation feature importance" not covered — only "feature attribution" is present), deliberately not remediated to avoid reproducing Revision note 3's over-broadening. Confirmed a recall strength: `[tiab]` indexing extends to MEDLINE author-keyword (OT) fields (PMID 36634916, retrieved via "SHAP" keyword absent from the visible abstract). Confirmed 3/8 candidates are correctly retrieved but fail Gate 1 of `inclusion_boundary.md` v2 (CT-scan-ordering, LOS, wait-time), validating the string's sensitivity-favouring design. New Known Limitations item 8 added. Term list unchanged; A+B+C remains FINAL. Pending: formal execution/export (item 10), decision-log entry (item 11). |
| v2 — PubMed formally executed | 2026-06-10 | A+B+C v2 FINAL string formally executed in PubMed with date range 2015/01/01–2026/06/10 (English). Returned **497 records**, exactly matching the live-verified design-time snapshot. Raw export saved as `data/searches/pubmed-explainabl-set.nbib`; `data/screening/prisma_counts.csv` PubMed Identification row updated (no longer DRAFT). Embase, IEEE Xplore, and ACM Digital Library executions remain pending (Next Steps item 10), to use the same 2026/06/10 upper bound. |
