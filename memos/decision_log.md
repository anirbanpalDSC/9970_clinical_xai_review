# Research Decision Log — Clinical XAI Systematic Review (9970)

Add an entry every time a search term changes, a criterion is refined, a coding dimension is added, or a methodological choice is made that a reviewer might probe. Never delete entries — append only.

Entry format:
```
## YYYY-MM-DD — [Short description]
**Decision:** What was decided
**Rationale:** Why (evidence, debate, constraint)
**Alternatives considered:** What else was on the table
**Impact:** What this changes (search / screening / extraction / synthesis)
**Defense if challenged:** How to respond during peer review or viva
```

---

## 2026-05-17 — Foundational XAI papers identified without systematic search

**Decision:** Seven canonical XAI theory papers used to ground operational definitions (issues #2, #5, #6) before the systematic search runs.

Papers:
- Lipton (2018) — *The Mythos of Model Interpretability*
- Doshi-Velez & Kim (2017) — *Towards a rigorous science of interpretable ML*
- Adadi & Berrada (2018) — *Peeking inside the black box*
- Rudin (2019) — *Stop explaining black box ML for high stakes decisions*
- Arrieta et al. (2020) — *Explainable AI: Concepts, taxonomies, opportunities*
- Miller (2019) — *Explanation in AI: Insights from social science*
- Samek et al. (2019) — *Explainable AI: Understanding, visualizing, interpreting DL*

**Rationale:** These papers represent field consensus — universally cited as foundational in XAI methodology. The systematic search is designed to identify primary clinical application studies, not theoretical foundations. Background/definitional literature is a distinct category in systematic review methodology and does not appear in the PRISMA count.

**Alternatives considered:** Running a separate Google Scholar search for foundational papers — rejected because it implies a second unsystematic search, which raises more methodological questions than it resolves during peer review.

**Impact:** Definitions committed to memos/terminology_instability.md will be anchored to these papers. Every operational definition in the extraction schema traces back to one of these sources.

**Defense if challenged:** "These papers were identified through domain expertise and field consensus, not the systematic search. The systematic search targets primary clinical XAI application studies. Background literature grounding our operational definitions is a standard and expected element of systematic review methodology. The decision to use these specific papers was logged prospectively on 2026-05-17, before the search ran, ruling out post-hoc selection."

---

## 2026-05-17 — Repo structure migrated from numbered folders to semantic layout

**Decision:** Replaced 00_Admin through 11_Research_Memos folder structure with docs/, data/, notebooks/, scripts/, references/, memos/, project_management/.

**Rationale:** Numbered folders encode sequence, not purpose. Semantic folders make the repository navigable to collaborators and reviewers without explanation. Markdown-first approach adopted for all protocol, memo, and synthesis documents.

**Alternatives considered:** Keeping numbered structure for familiarity — rejected because it does not scale and obscures the function of each directory.

**Impact:** All future file paths in issues, protocol, and scripts follow the new structure. CLAUDE.md updated with structure table.

**Defense if challenged:** Not applicable — internal infrastructure decision, not a methodological one.

---

## 2026-05-17 — GitHub issues scoped to Milestones 1–3 only

**Decision:** Filed 17 issues covering concept stabilization, infrastructure, search, and screening (Weeks 1–3). Milestones 4–7 (extraction, framework, manuscript, submission) exist but have no issues yet.

**Rationale:** Filing extraction and synthesis issues before screening is complete is premature. The coding rubrics built in Week 1 determine what extraction issues look like. Pre-filing them risks locking in dimensions before the literature is understood.

**Alternatives considered:** Filing all issues upfront for full project visibility — rejected because it creates false precision and issues that will need to be rewritten after the concept layer is established.

**Impact:** Issues for Milestones 4–7 will be filed after screening is complete and the extraction schema is piloted on included papers.

**Defense if challenged:** Not applicable — internal project management decision.

---

## 2026-05-17 — Reference management infrastructure: Zotero linked to Google Drive

**Decision:** PDFs stored in Google Drive, linked into Zotero. Zotero is the single source of truth for paper metadata, tags, and citations.

**Rationale:** PDFs are binary files — they do not belong in Git. Google Drive provides cloud storage and access across devices. Zotero bridges the gap: it manages metadata, enables BibTeX export into the repo, and supports annotation and tagging without polluting version control with large files.

**Alternatives considered:**
- PDFs directly in repo — rejected (binary files break Git workflows, inflate repo size)
- Google Drive only — rejected (no structured metadata, no BibTeX export, no tagging)
- Zotero cloud storage only — acceptable but Google Drive link retained for existing files

**Impact:**
- `references/bib/` in repo will be populated by Zotero BibTeX exports, not manual entry
- `references/annotated/` will hold structured reading notes keyed to Zotero item keys
- PDFs are not tracked by Git; the `.gitignore` covers common document formats

**Defense if challenged:** Not applicable — internal infrastructure decision. PDFs available on request via Google Drive; metadata and citations are version-controlled in the repo.

---

## 2026-05-23 — Inclusion boundary: clinical vs medical vs healthcare AI

**Decision:** Three-gate decision rule defining in-scope "clinical AI" for this review.
- Gate 1: AI operates in a clinical/medical domain (diagnosis, prognosis, treatment, risk, monitoring, imaging, pathology). Excludes administrative, consumer, drug discovery, population analytics.
- Gate 2: AI output informs an individual patient care decision. Excludes population analytics and clinical trial infrastructure. Clinical trial sub-rule: include if the trial evaluates the AI tool as a clinical intervention; exclude if AI operates the trial.
- Gate 3: A licensed clinician is involved at any stage of the decision pathway (review, validation, action, or override). Excludes fully automated systems. Asynchronous review satisfies this gate.

**Rationale:** "Clinical," "medical," and "healthcare" AI are not synonyms. Without an explicit boundary, screening decisions drift across reviewers. The three-gate structure forces a consistent sequence of checks and makes borderline cases documentable rather than judgment-dependent.

**Alternatives considered:**
- Broader: any AI used in a healthcare organisation — rejected because it sweeps in administrative AI (scheduling, billing) that has no clinical decision content.
- Narrower: require real-time clinician-AI interaction — rejected because batch/asynchronous review (e.g., radiologist reviewing AI-flagged worklist) is clinically valid and excludes too much literature.
- Exclude all clinical trials — rejected because trials that evaluate AI as a clinical decision support intervention are primary evidence for this review; excluding them would omit important deployment studies.

**Impact:** Applies to title/abstract screening, full-text screening, and extraction. Borderline cases must be documented in decision_log.md with paper title and rationale.

**Defense if challenged:** "We distinguished clinical from administrative and consumer AI using three sequential gates, each of which can be independently verified from paper methods sections. The boundary was committed to the protocol before screening began and logged prospectively on 2026-05-23. The clinical trial sub-rule follows standard systematic review practice of distinguishing interventions under study from study methodology."

---

## 2026-05-17 — BibTeX export settings and file cleanup

**Decision:** Exported foundational papers from Zotero with Export Notes unchecked, Export Files unchecked, Use Journal Abbreviation unchecked, Character Encoding UTF-8. Machine-specific `file = {...}` fields stripped before committing. Missing years added for Lipton and Samek.

**Rationale:**
- Export Notes unchecked: personal working notes are not citation metadata; they pollute the BibTeX file
- Export Files unchecked: PDFs stay in Google Drive, not in Git
- Use Journal Abbreviation unchecked: full journal names are unambiguous; abbreviation style is applied by the manuscript template, not the source BibTeX
- `file = {...}` fields stripped: contained absolute Google Drive paths (`G:\My Drive\...`) which are machine-specific and non-portable
- Lipton corrected to 2018 (Queue journal publication of the 2016 arXiv preprint)
- Samek corrected to 2017 (ITU Journal; previously listed as 2019 in this log — that was an error)

**Alternatives considered:** Keeping file paths for personal convenience — rejected because the `.bib` file is version-controlled and shared; portability takes precedence.

**Impact:** `references/bib/foundational.bib` is now clean, portable, and citation-ready for LaTeX/Pandoc. Standard practice for all future BibTeX exports from this project.

**Defense if challenged:** Not applicable — internal infrastructure decision.

---

## 2026-05-26 — Custom quality rubric adopted over QUADAS-2, RoB 2, TRIPOD

**Decision:** Developed a bespoke five-dimension quality rubric (QR1–QR5, scored 0–2 each) rather than applying any standard quality assessment tool directly. Retained specific elements from QUADAS-2, RoB 2, and TRIPOD through adaptation; rejected the remainder. Rubric committed to `data/coding/quality_rubric.md`.

Adopted elements:
- QUADAS-2 Patient Selection domain adapted into QR1 (Participant Appropriateness): same concern but operationalised as participant-to-claim match rather than a selection bias domain
- QUADAS-2 Reference Standard domain adapted into QR4 (Explanation Faithfulness): reference standard for an XAI explanation is the model's actual computation; requires a ground truth comparison, not face validity
- RoB 2 D4 (Outcome Measurement) adopted as the foundation for QR3 (Outcome Measurement): validated instruments required for the primary outcome
- RoB 2 D5 (Selective Reporting) and TRIPOD reporting requirements absorbed into QR5 (Reporting Completeness)

Rejected elements:
- QUADAS-2 Index Test and Flow/Timing: structurally inapplicable — no diagnostic test threshold; no patient-level flow across tests
- RoB 2 D1 (Randomisation), D2 (Deviations), D3 (Missing Data): applicable only to RCTs; fewer than 10% of clinical XAI papers are RCTs (H5)
- TRIPOD calibration, discrimination, validation type: predictive model properties, not XAI evaluation properties

New dimensions with no standard tool equivalent:
- QR4 (Explanation Faithfulness): entirely absent from QUADAS-2, RoB 2, and TRIPOD — most consequential gap given that unfaithful explanations in clinical settings may increase confidence without warranting it
- QR5 partially covers XAI-specific reporting requirements not in TRIPOD (which covers the underlying model but not the explanation system)

**Rationale:** No existing quality tool was designed for XAI evaluation papers. Direct application of QUADAS-2 or RoB 2 would be a category error: QUADAS-2 assumes a diagnostic accuracy study design; RoB 2 assumes a randomised trial. Both tools would leave the most critical XAI-specific quality concerns unaddressed. TRIPOD is a reporting guideline for predictive models, not an evaluation quality tool. Developing a custom rubric is consistent with systematic review methodology when no validated tool exists for the study type.

**Alternatives considered:**
- Apply QUADAS-2 to all papers regardless of study type — rejected because forced application produces low-informativeness scores for user studies and proxy-metric papers
- Apply RoB 2 to RCTs and QUADAS-2 to user studies — rejected because it creates non-comparable quality scores across papers; synthesis requires a uniform instrument
- Apply GRADE certainty of evidence — rejected because GRADE is designed for bodies of evidence supporting clinical recommendations, not for primary study quality assessment in a methodological review

**Impact:** Six new columns added to extraction schema (`QR_Participant`, `QR_Task`, `QR_Outcome`, `QR_Faithfulness`, `QR_Reporting`, `QR_Notes`); schema is now v1.2 (33 columns). Quality scores will be used in sensitivity analyses (e.g., re-running H1 and H3 restricted to QS_Total >= 7 papers) and to characterise the quality distribution of the included literature.

**Defense if challenged:** "Standard quality assessment tools are not designed for XAI evaluation studies, which span proxy-metric papers, user studies, simulation studies, and deployment studies — none fitting the RCT or diagnostic accuracy designs those tools assume. We reviewed each standard tool systematically (logged prospectively in `memos/decision_log.md` on 2026-05-26) and adopted elements that map onto XAI evaluation designs while developing two new dimensions — Explanation Faithfulness and Reporting Completeness — absent from existing tools but representing the primary methodological failure modes in XAI evaluation research."

---

## 2026-06-07 — PubMed search string v1 finalized: precision-tuned and recall-validated (9,672 hits)

**Decision:** Adopted a precision-tuned version of the Concept-A (XAI/interpretability) term block as the final v1 PubMed search string, after diagnosing three successive structural problems and validating recall against an independently assembled benchmark. Final string: `(Concept A: 24 XAI/interpretability term-groups) AND (Concept B: clinical-context terms) AND (2015–2024) AND (English)`, returning **9,672 hits**. Full diagnostic trail recorded in `docs/protocol/search_string_pubmed_v1.md` (Revision notes 1–3).

**Diagnostic sequence:**
1. Original draft returned 9 hits — caused by an accidental nested 3-way AND (Concept B contained a redundant "generic AI/ML present" sub-block ANDed against the clinical-context sub-block). Fixed by flattening Concept B to a single OR block, restoring the intended two-concept design.
2. Corrected string returned 36 hits in the user's first re-run — caused by (a) a leftover duplicate `AND AND` syntax artifact and (b) PubMed's phrase-index rejecting `"prototype-based explanation*"[tiab]`, compounded by (c) four PubMed sidebar filters (Review, Systematic Review, Aged 65+, Humans) silently stacked on top of the string in the UI. None of these were string-design problems; (c) alone would have suppressed the vast majority of primary-research hits.
3. With filters cleared and syntax fixed, the string returned 15,385 hits — too broad to screen by hand. Diagnostic isolation (Concept A run alone = 70,946 hits) showed Concept A contained five generic ML/statistics term-groups (`"black box"`, `"attention map*"/"attention weight*"/"attention mechanism*"`, `"saliency map*"`, `"feature importance"`, `"decision rule*"`) that match enormous numbers of non-XAI papers (transformer architecture papers, random-forest variable-importance papers, clinical-prediction-rule papers, etc.). Removing them yielded 9,672 hits (37% reduction, ~5,700 fewer hits).

**Recall validation:** The protocol's plan to validate against "the seed paper set used for EV/quality rubric piloting" (per the original Issue #16 framing in the search-string doc) turned out to reference a set that does not exist yet — `docs/osf/preregistration_draft.md` and `memos/research_master_memo.md` both specify that seed papers are drawn from *included* papers *after* full-text screening, which would make using them to validate the search circular. `references/bib/foundational.bib` was also ruled out — its 7 entries are general XAI theory/survey papers (Lipton, Rudin, Miller, Doshi-Velez, Adadi, Arrieta, Samek), none of which would pass Gate 1 of `inclusion_boundary.md` as standalone clinical-application studies.

An independent benchmark was instead built by citation-chasing forward from those 7 foundational papers via the Semantic Scholar citations API, filtering for clinical-domain + XAI-method co-occurrence in titles, restricted to 2019–2023 publication years (so the search's own date filter wouldn't manufacture artificial "misses"). Eight candidates were screened against the three `inclusion_boundary.md` gates on abstract content; four passed clearly:
- Cao, Kunaprayoon & Ren (2023), PMID 37543055 — interpretable CNN for radiosurgery dose prescription, brain metastases (physician-ranking validation reported)
- Tosun et al. (2020), PMID 32541594 — "Explainable AI (xAI) for Anatomic Pathology" / HistoMapr (designed as a pathologist's interactive guide)
- Kumar et al. (2021) — "Doctor's Dilemma": CAM-based CNN for brain tumor diagnosis (doctor feedback and physician trust evaluation reported); published in ACM Trans. Multimedia Computing — not in PubMed
- Gu et al. (2020/2023) — xPath human-AI pathology diagnosis tool (evaluated with 12 medical professionals); published in ACM Trans. Computer-Human Interaction — not in PubMed

Both MEDLINE-indexed benchmark papers (PMID 37543055, 32541594) were tested against both the 15,385-hit and 9,672-hit string variants via the PubMed E-utilities API: **both papers are retrieved by both variants**, confirming the five removed term-groups cost zero recall against this benchmark. (Notably, the Anatomic Pathology paper's abstract contains "black-box" — a removed term — yet still matches via "xAI"/"explainable AI", demonstrating the removed term was redundant for this paper.)

**Secondary finding — database coverage gap:** Of the six benchmark candidates checked against PubMed (the 4 gate-passing papers above plus 2 borderline candidates — Nayebi et al. 2022 TBI XAI-comparison, AMIA/arXiv; Clough et al. 2019 Cardiac MRI interpretability, MICCAI/arXiv), only 2/6 (33%) are indexed in MEDLINE. The other 4 are published in ACM Digital Library, MICCAI proceedings, and AMIA-symposium/arXiv-preprint venues that MEDLINE simply does not cover — a structural limitation no query refinement can overcome. This is concrete empirical evidence supporting the multi-database search plan (Issue #22), and these four papers are now earmarked as retrievability test cases for the ACM Digital Library / IEEE Xplore translations of the string.

**Rationale:** Sensitivity-favouring systematic review search design requires casting a wide net on the two concepts that reliably appear in abstracts (XAI vocabulary, clinical-context vocabulary) while letting screening criteria do precision work — but "wide net" does not mean "include every generic ML term," since terms that are not XAI-specific in ordinary usage (attention mechanisms, black box, feature importance, decision rules) inflate the corpus with papers screening would reject anyway, at substantial reviewer-time cost. Validating the cut against an independent, pre-screening benchmark — rather than trusting the diagnostic logic alone — is what makes the 9,672 figure defensible rather than a guess.

**Alternatives considered:**
- Keep the original 5 generic terms "just in case" — rejected: the benchmark validation found they retrieved nothing the more specific terms didn't already retrieve, while adding ~5,700 hits requiring manual screening
- Use the post-screening IRR seed-paper set for this validation — rejected as circular (see above); the benchmark had to be assembled independently and *before* the search is executed for record
- Treat the 15,385-hit string as final on the grounds that "more sensitivity is always better" — rejected: reviewer time is a real constraint (PRISMA screening burden), and the diagnostic data showed the extra ~5,700 hits were predominantly noise, not missed recall

**Impact:** `docs/protocol/search_string_pubmed_v1.md` now records the final, validated string (9,672 hits) as the version to execute and report in PRISMA Identification. Four named papers (Kumar et al., Gu et al., Nayebi et al., Clough et al.) are flagged as concrete test cases for the Issue #22 multi-database translation work.

**Defense if challenged:** "The final search string was not accepted on first principles alone — it went through three documented diagnostic cycles (9 → 36 → 15,385 → 9,672 hits), each traced to a specific, named cause (structural AND-nesting error, syntax/filter artifacts, generic-term over-inclusion), and the final cut was validated against an independently assembled benchmark of papers that satisfy all three protocol-defined inclusion gates, built via citation-chasing rather than drawn from the search's own results (which would have been circular). The validation additionally surfaced — and we have pre-registered our awareness of — a database-coverage limitation of MEDLINE that motivates the planned multi-database search, with concrete papers identified as translation test cases."

---

## 2026-06-08 — Retracted publications screened out as a pre-registration QC step (11 records, distinct from content-based screening)

**Decision:** Before title/abstract screening begins, 11 records from the 9,672-hit PubMed pull (search executed and logged 2026-06-07) were identified as formally retracted and removed from the active screening pool as a discrete pre-screening QC step — tracked separately in `data/screening/prisma_counts.csv` from both deduplication and the E1–E6 content-based exclusion taxonomy in `screening_fulltext_criteria.md`. Full record-level detail (PMID, title, original publication date, DOI, and retraction-notice citation) is preserved in `data/screening/retracted_records_pubmed_2026-06-08.csv` — records are flagged and tagged `retracted-excluded` in Zotero, not deleted, to keep the audit trail intact.

**Rationale:** Retraction status is a structural/integrity property of a record, not a content-relevance judgment — it doesn't map onto any of the E1–E6 full-text exclusion codes (which assess clinical-domain fit, XAI presence, evaluation rigor, publication type, extraction sufficiency, or duplication), and it can't be assessed from title/abstract content the way Gate 1–3 criteria can. Screening it separately, before formal screening starts, prevents reviewer time being spent on records that cannot be included in synthesis regardless of topical fit (per PRISMA/Cochrane/COPE guidance: retracted findings should not be carried into evidence synthesis, but their presence in the search must be documented transparently rather than silently dropped).

Retraction status was confirmed directly from NLM/MEDLINE indexing — the `RIN` ("Retraction in") field and `PT - Retracted Publication` publication-type tag in the raw `.nbib` export — rather than relying solely on Zotero's Retraction-Watch-Database integration, which initially surfaced only 10 of the 11 (likely a sync-lag gap; MEDLINE's own field-level retraction linkage is the more authoritative and immediately-available source for this corpus).

**Two findings emerged from this check that are independently worth recording:**

1. **A cluster of the retractions traces to the 2023 Hindawi/Wiley mass-retraction event** (a publicly documented paper-mill/compromised-peer-review scandal): of the 11, five were published in *J Healthc Eng* (×2), *Comput Math Methods Med* (×2), and *Comput Intell Neurosci* (×1) — all Hindawi titles caught up in that wave — with retraction notices issued 2023–2025. Several of these have titles squarely on-topic for clinical XAI (e.g., "Explainable AI in Diagnosing and Anticipating Leukemia Using Transfer Learning", "PSCNN: PatchShuffle Convolutional Neural Network for COVID-19 Explainable...", "PSSPNN: PatchShuffle Stochastic Pooling Neural Network for an Explainable..."). This indicates that a non-trivial share of literature superficially matching "clinical XAI" search criteria may originate from compromised peer-review pipelines — a publication-integrity risk worth flagging as a documented limitation of database-derived corpora in this domain, and worth keeping in mind during full-text quality assessment (Issue #20 rubric) as a venue-level signal to watch for in borderline cases.
2. **One record (PMID 28946087, "Beneficial effect of mixture of additives amendment on enzymatic activities...") is an off-topic false-positive search match** — an agricultural/soil-microbiology paper with no clinical-AI content, which would have failed Gate 1 at screening regardless of its retraction status. Retained in the retracted-records log for completeness and as a documented example of the kind of incidental term-overlap false positive the search string is expected to produce (to be filtered at title/abstract screening in the ordinary course).

**Alternatives considered:**
- Leave retracted records in the active pool and exclude them during full-text screening under a generic "wrong publication type" code (E4) — rejected: this would cost reviewer time screening records that are deterministically excludable pre-screening, and would blur a structural/integrity exclusion with content-based exclusion reasons in the PRISMA reporting, making the E1–E6 breakdown harder to interpret
- Silently delete retracted records from the corpus without logging — rejected outright: undermines the methodological-transparency standard this review follows throughout (every removal in this project is logged with PMIDs and rationale, per the search-string revision notes and this log's own header instruction to never delete without a record)
- Trust Zotero's Retraction Watch Database flag alone (10 records) — rejected in favour of cross-checking against MEDLINE's own `RIN`/`PT` fields, which surfaced an 11th record Zotero missed; the raw NLM metadata is the more authoritative and immediately current source for this specific corpus

**Impact:** `data/screening/prisma_counts.csv` now carries an explicit "Retracted publications removed (pre-screening QC)" row (count: 11) positioned in the Identification stage, between duplicate-removal and the post-cleanup "Records after deduplication" total — which has been redefined to subtract both duplicates and retracted records. `data/screening/retracted_records_pubmed_2026-06-08.csv` provides full record-level traceability (PMIDs, titles, retraction-notice citations) for PRISMA reporting and potential reviewer queries. The Hindawi-cluster observation is a candidate addition to the manuscript's limitations section and a venue-level watch-flag for the Issue #20 quality rubric during full-text assessment.

**Defense if challenged:** "Retracted publications were not silently dropped from the corpus — all 11 were identified via NLM's own MEDLINE retraction-linkage fields (cross-checked against, and found more complete than, Zotero's Retraction Watch Database integration), logged individually with PMIDs and retraction-notice citations in `data/screening/retracted_records_pubmed_2026-06-08.csv`, and removed at a documented pre-screening QC stage — distinct from both deduplication and our content-based E1–E6 exclusion taxonomy — because retraction is a structural integrity property, not a relevance judgment, and standard guidance (PRISMA/Cochrane/COPE) holds that retracted findings should not enter evidence synthesis. We additionally used this check to surface and document a publication-integrity risk specific to this literature (a cluster of papers from the 2023 Hindawi mass-retraction event with on-topic titles), which we treat as a transparency strength of our screening process rather than a problem to be hidden."

---
