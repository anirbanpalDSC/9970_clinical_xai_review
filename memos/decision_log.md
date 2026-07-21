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

## 2026-06-09 — First-pass DRAFT/UNTESTED translations of the search string for Embase, CINAHL, IEEE Xplore, and ACM Digital Library (Issue #22)

**Decision:** Created four new protocol documents — `docs/protocol/search_string_embase_v1.md`, `search_string_cinahl_v1.md`, `search_string_ieee_v1.md`, `search_string_acm_v1.md` — each translating the finalized PubMed v1 rev 3 string (9,672 hits; see 2026-06-07 entry above) into the field-tag/Boolean syntax of the respective database. All four are explicitly marked **DRAFT / UNTESTED**: none have been run against a live database yet. They were written now, ahead of live execution, because the user has two remaining days before a week away from this development environment (office-laptop access only, with web access to github.com and claude.ai but not this session/repo clone).

**Rationale:** The translation work — mapping field tags ([tiab] → :ti,ab,kw / TI+AB / Title+Abstract+Keyword fields), converting MeSH terms to Emtree/CINAHL-Heading equivalents or dropping them where no clinical controlled vocabulary exists (IEEE, ACM), and applying the precision-tuning lessons from the PubMed diagnostic history (Revision notes 1–3) — depends on full conversational context (the validated Concept A/B term lists, `inclusion_boundary.md` gates, `xai_method_taxonomy.md`, and the specific over-broadening and filter-stacking failure modes already diagnosed once for PubMed). That context does not need to be re-derived during the office-laptop week if the drafts are written now. The remaining work — running each string live, resolving "to verify" items (Emtree term existence, CINAHL Subject Heading labels, IEEE/ACM custom-query syntax, wildcard behaviour), and recording hit counts — requires live database access, which the office laptop is *better* positioned to provide (likely better institutional subscriptions) than this environment.

**Key translation decisions baked into the drafts:**
- **Embase:** field tag `:ti,ab,kw` (broader than PubMed's [tiab] by design — includes author keywords); 5 MeSH terms mapped to unverified Emtree candidates (`'doctor'/exp` for "Physicians", `'decision making'/exp` for "Clinical Decision-Making", etc.) with an explicit warning not to add broad Emtree explosions (`'machine learning'/exp`, `'artificial intelligence'/exp`) to Concept A, given the PubMed precision-tuning history (70,946 hits for an unconstrained Concept A).
- **CINAHL:** `TI (...) OR AB (...)` block structure (no single [tiab]-equivalent field code); 5 MeSH terms mapped to CINAHL Subject Heading candidates, flagging "Decision Making, Clinical" (word-order-reversed from MeSH's "Clinical Decision-Making") as most likely to need correction.
- **IEEE Xplore:** all 5 MeSH terms dropped (no clinical controlled vocabulary); two candidate query forms offered — Option 1 (unrestricted Command Search, broader than [tiab], recommended as first test) and Option 2 (field-restricted to Document Title/Abstract/Author Keywords, syntax unverified). No confirmed retrievability benchmark exists for IEEE — none of the 4 non-MEDLINE benchmark papers (Kumar, Gu, Nayebi, Clough) are IEEE-published.
- **ACM Digital Library:** all 5 MeSH terms dropped; bracket-nested `[Field: (...)]` custom-query syntax proposed but unverified, with wildcard (`*`) behaviour also flagged as unverified (with a manual-variant-expansion fallback). Kumar et al. (2021, ACM Trans. Multimedia) and Gu et al. (2020/2023, ACM Trans. CHI) — both confirmed ACM DL content — are the primary retrievability test cases for this database.

**Alternatives considered:**
- Defer all translation work until after the office-laptop week, when live testing could happen immediately — rejected: the *translation* (mapping syntax and controlled vocabulary, applying precision lessons) is the part most dependent on this session's accumulated context, while the *live testing* is the part the office laptop is well-suited for regardless of context. Splitting the work this way uses the two remaining days for the higher-context-dependency task.
- Wait until each database's controlled-vocabulary terms could be verified live before writing anything — rejected: would have produced no artifact at all before departure; the chosen approach instead produces a fully-specified draft with every uncertain element explicitly flagged and a documented fallback, so live testing during the office-laptop week is a verification/iteration task rather than a from-scratch drafting task.

**Impact:** `docs/protocol/search_string_pubmed_v1.md` Next Steps item 4 updated to mark database translation as done (drafts created) and a new item 5 added (run drafts live, resolve flagged items, record hit counts in `data/screening/prisma_counts.csv`). All four new documents are self-contained with their own Known Limitations and Next Steps sections so they can be acted on independently during the office-laptop week without needing this conversation's context.

**Defense if challenged:** "These four translations are explicitly labeled DRAFT/UNTESTED and are not reported as PRISMA Identification counts — `data/screening/prisma_counts.csv` retains empty cells for Embase/CINAHL/IEEE/ACM pending live execution. Producing the drafts now was a deliberate sequencing choice: the syntax-mapping and precision-tuning judgment calls (which controlled-vocabulary terms to include/exclude, how to handle databases with no clinical thesaurus) depend on the full diagnostic history already established for the PubMed string, and writing them down now avoids re-deriving that reasoning later. Every uncertain syntax element (Emtree term existence, CINAHL heading labels, IEEE/ACM query syntax, wildcard behaviour) is explicitly flagged with a verification step and a fallback, so the live-testing phase is bounded and checklist-driven rather than open-ended."

---

## 2026-06-09 — Date range kept at 2015–2024 (9,672); 2025+ deferred to a planned pre-submission search update

**Decision:** Investigated extending the search date range beyond 2024 (motivated by wanting to capture the most recent literature before a week away from this environment), but **kept the already-validated 2015–2024 / 9,672-hit PubMed result as-is**. No re-pull was performed. Instead, `docs/osf/prospero_draft.md` (Searches section) and `docs/osf/preregistration_draft.md` (Eligibility Criteria, Publication period) were both updated to explicitly document a **planned search update covering January 2025 onward, to be run across all five databases shortly before manuscript submission**.

**Investigation (PubMed, same validated Concept A/B query, English, run 2026-06-09):**

| Window | Hit count |
|---|---|
| 2015–2024 (current registered/logged) | 9,672 |
| 2015–2026/06/30 (full extension to "now") | 22,406 (+131%) |
| 2022–2026/06/30 (shifted window) | 19,796 (+105%) |
| 2025 alone | 8,144 |
| 2026 Jan–Jun alone | 5,861 |
| 2015–2021 (would be dropped if shifting to 2022–2026) | 2,785 |

**Rationale:**
1. **The 2025–2026 surge dominates regardless of start date.** 2025 alone (8,144) is nearly as large as the entire 2015–2024 decade (9,672), and Jan–Jun 2026 alone (5,861) already exceeds half of 2025's full-year count. Any window including 2025–2026 roughly doubles the corpus (~20–22k vs. 9,672) — a major screening-burden change, not a minor search-string tweak.
2. **Shifting the start date to 2022 doesn't solve this and costs more.** 2022–2026/06/30 (19,796) is barely smaller than 2015–2026/06/30 (22,406) — the saving is only the 2,785 records from 2015–2021, which `docs/osf/prospero_draft.md`'s existing rationale specifically defends as the "early adoption period" for SHAP/LIME/Grad-CAM (these methods emerged 2016 onward). Shifting would mean rewriting that rationale to drop records it was written to protect, for a ~12% reduction in total burden.
3. **A partial mid-2026 pull would need to be redone anyway.** Today (2026-06-09), a "2026/06/30" cutoff only reflects records indexed through today — the rest of June doesn't exist yet. More importantly, very recent records' `Date - Publication` fields are subject to Epub-ahead-of-print reclassification (the same kind of date-field instability noted for PMID 38142755's retraction notice in the 2026-06-08 entry above), so a 2025–2026 pull done now would not be stable and would need re-verification before being reported. Running the update search later (closer to submission) captures the *complete*, *stable* 2025–2026+ window in one pass — capturing more of "the latest movement in the field" than a partial pull today, not less.

**Alternatives considered:**
- Extend to 2015–2026/06/30 now (22,406) — rejected: requires re-pulling ~2.3x the records (≈56 efetch batches vs. 25), and rewriting `search_string_pubmed_v1.md`, all four new database-translation drafts, `prisma_counts.csv`, and the PROSPERO/preregistration date-range text, all under a 2-day deadline — and the result would need re-verification later regardless (see Rationale point 3).
- Shift to 2022–2026/06/30 (19,796) — rejected: similar burden to full extension, but additionally requires rewriting the PROSPERO early-adoption-period rationale to justify dropping 2015–2021 records that rationale currently protects.
- Do nothing / don't document a future update — rejected: would leave 2025–2026 as a silent gap with no documented plan to address it, inviting exactly the "don't we miss the latest movement in the field?" objection this entry exists to pre-empt.

**Impact:** No change to `search_string_pubmed_v1.md`, `prisma_counts.csv`, or any of the four new database-translation drafts — all remain correct at 2015–2024. `docs/osf/prospero_draft.md` (Searches section, after the Date range line) and `docs/osf/preregistration_draft.md` (Eligibility Criteria, Publication period) now both state the 2015–2024 initial search range *and* an explicit commitment to a January-2025-onward update search across all five databases shortly before submission, with the 8,144/5,861/2026-instability data point cited as the rationale for why "later" captures more than "now."

**Defense if challenged:** "We did not arbitrarily cap the search at 2024 out of inertia — we explicitly scoped what extending to mid-2026 would mean (22,406 hits, +131%; or 19,796 if the window were shifted instead of extended, +105%), found that the 2025–2026 surge alone (≈14,000 hits across 18 months) exceeds the entire prior decade, and determined that a partial pull today would be both incomplete and unstable due to Epub-ahead-of-print date reclassification. We therefore kept the validated 2015–2024/9,672 result and made an explicit, registered commitment to a pre-submission update search covering 2025 onward — the standard PRISMA mechanism for exactly this situation, which will capture the recent surge completely and with stable dates rather than partially and provisionally."

---

## 2026-06-10 — Pivot back to original proposal scope: EM/ED-only XAI scoping review (RQ1–RQ3, PRISMA-ScR/JBI), de-scoping the cross-domain 6-hypothesis systematic review

**Decision:** Revert Project 9970's scope to the original Summer Research Proposal ("Beyond Fidelity: Evaluating the Validity of Explainable AI in Emergency Triage — A Scoping Review," April 2026): an Emergency-Medicine-only scoping review of XAI methods applied to ED-encounter decisions (initial patient intake, ESI/acuity scoring, immediate disposition), addressing RQ1 (which post-hoc explanation methods are deployed and what justification is given for method selection), RQ2 (how explanation effectiveness is evaluated across levels of human involvement, and what this reveals about evaluation rigor), and RQ3 (what evaluation evidence would satisfy regulatory interpretability-validation expectations under FDA AI/ML guidance and EU AI Act Article 13). Methodology shifts from a PRISMA systematic review with 6 confirmatory hypotheses to JBI scoping review methodology (Peters et al., 2020) + PRISMA-ScR reporting (Tricco et al., 2018), with narrative synthesis organised by RQ.

The conceptual upgrades developed during the exploratory phase — the trust-calibration-vs-plausibility distinction (Issue #3) and the 4-dimension ecological validity rubric (Issue #5) — are preserved and applied to the narrower EM corpus, replacing the original proposal's looser "interpretability validity" definitions with the more rigorous operationalisations already built out.

**Context:** Conclusion of a multi-turn strategic discussion (progress report → scope-mismatch identification against the uploaded original proposal PDF → comparison → advisor framing → "balance of 8 weeks vs noteworthy publication" recommendation). The repo's built-out scope (cross-domain, 6-hypothesis, 5-database systematic review) had organically diverged from the original graded-program proposal (EM-only scoping review, RQ1–RQ3, regulatory framing, 4 databases, JBI/PRISMA-ScR). User confirmed: "Yes. I need to immediately pivot back."

**Rationale:**
1. The 8-week single-reviewer timeline (graded program, proposal Table 1 rubric) cannot support a cross-domain corpus sized for confirmatory hypothesis testing (current PubMed-only count: 9,672 records, cross-domain) plus 4–5 database translations plus full extraction/IRR/synthesis/manuscript. An EM-narrowed corpus is the only configuration realistically completable within Phase 2/3.
2. The grading rubric's largest-weighted criterion (Analysis & Synthesis, 25%) explicitly rewards "argue, not summarize." Narrative synthesis organised around RQ1–RQ3 with a regulatory-readiness argument is a stronger fit for this than reporting null/non-null results across 6 pre-registered hypotheses on a corpus that may not reach adequate cell counts for several of them (H4, H6 were already flagged as at-risk for underpowered cells even in the larger cross-domain corpus).
3. The regulatory framing (FDA AI/ML guidance, EU AI Act Article 13 — a 2024 regulation) is novel and timely, gives the EM-narrowed scope a publication hook the broader cross-domain framing lacked, and matches the original proposal's explicit framing of this review as "scaffolding for empirical studies planned in later semesters."
4. Work invested so far is not wasted: the trust-calibration/plausibility distinction and 4-D EV rubric are direct upgrades over the original proposal's looser constructs and slot into the EM-only corpus without modification; the 6-type Eval_Type taxonomy (Issue #8) and its existing mapping to Doshi-Velez & Kim (2017) gives a head start on RQ2/RQ3's framework-classification requirement.

**What is preserved (applied to the narrower EM corpus as upgrades over the proposal's original definitions):**
- Trust calibration vs. explanation plausibility distinction (Issue #3, `memos/conceptual_distinctions.md`) — replaces the proposal's single undifferentiated "trust calibration" construct; feeds RQ3's trust-calibration-under-varying-performance criterion.
- 4-dimension ecological validity rubric (EV_Participant / EV_Task / EV_Environment / EV_Outcome, Issue #5) — retained as a secondary/exploratory lens on RQ2's evaluation-rigor question, alongside the proposal's 5-level evaluation taxonomy (computational, proxy, simulated, clinician-in-the-loop, deployment).
- Workflow realism rubric (Issue #4) and 5-dimension QR1–QR5 quality/RoB rubric (Issue #20) — repositioned as supplementary/exploratory analyses feeding the RQ2 narrative synthesis, not primary confirmatory tests.
- 6-type Eval_Type taxonomy (Issue #8) and its mapping to Doshi-Velez & Kim (2017)'s 3-category framework (`memos/research_master_memo.md`) — becomes the operational basis for the RQ2/RQ3 framework-classification fields.
- 21-tag semantic vocabulary (Issue #13).
- OSF pre-registration as the primary registration record (filed 2026-05-24).

**What changes:**
- Inclusion boundary (`docs/protocol/inclusion_boundary.md`, Issue #7) rewritten from the cross-domain 3-gate rule (clinical domain / individual decision / clinician-in-loop) to an EM-only 3-gate rule: (1) decision point occurs during the initial ED encounter — intake, ESI/acuity scoring, or immediate disposition, explicitly excluding pre-hospital EMS triage, inpatient ward monitoring, and ICU management even when the study population originates in the ED; (2) an explainable/interpretable AI method is applied; (3) an empirical evaluation component (computational, proxy, simulated, clinician-in-the-loop, or deployment) is reported.
- Research questions replaced: the prior 1 primary + 5 secondary cross-domain questions are replaced with RQ1 (methods deployed + selection justification), RQ2 (evaluation-level distribution and rigor), RQ3 (regulatory-readiness evidence against FDA AI/ML guidance + EU AI Act Article 13). `docs/osf/preregistration_draft.md` to be rewritten accordingly.
- H1–H6 confirmatory hypotheses (`memos/synthesis_hypotheses.md`) repositioned as supplementary/exploratory analyses feeding the RQ2 narrative synthesis — not pre-registered confirmatory tests with their own significance thresholds.
- Database scope reverts to the proposal's 4 databases (PubMed, Embase, IEEE Xplore, ACM Digital Library); CINAHL dropped from the primary search. The cross-domain expansion to 5 databases was driven by the broader population/context scope, which no longer applies. CINAHL may be retained as a supplementary/sensitivity source if Phase 3 has spare time, but is not part of the primary PRISMA-ScR flow.
- PubMed search string (`docs/protocol/search_string_pubmed_v1.md`, v1 rev 3, 9,672 hits, cross-domain) gets a new Concept C (EM/ED-encounter terms — emergency department/room, triage, ESI/acuity scoring, disposition, patient intake) ANDed with the existing Concept A (XAI) and Concept B (clinical context), narrowing the corpus to EM-specific records. New hit count to be logged once tested.
- Embase/IEEE/ACM draft translations (Issue #22, including the paused 108,886-hit ACM diagnostic) are superseded — they will need Concept C added and re-derivation once the new PubMed Concept C is validated. The CINAHL translation is shelved per the database-scope change above.
- Extraction schema (`data/extraction/schema_v1.csv`, v1.2 → v1.3) gains 10 new columns: `Method_Justification_Type`, `Method_Justification_Notes` (RQ1, inductive coding: Computational / Cognitive / Workflow / Mixed / NotReported); `Method_Interface_Isolated` (whether explanation-method effects are isolated from interface/presentation effects); `DoshiVelez_Category`, `VilonLongo_Category` (framework classification, RQ2/RQ3 — Vilone & Longo controlled vocabulary to be finalised during the 5-paper extraction pilot); `Reg_Comprehension`, `Reg_TrustCalibration`, `Reg_UncertaintyTransparency`, `Reg_WorkflowSafety`, `Reg_Notes` (RQ3's four regulatory-evidence criteria).
- PROSPERO (`docs/osf/prospero_draft.md`, Issue #19) deprioritised/paused — the proposal's registration requirement is OSF only; PROSPERO submission is not required by the grading rubric, and the draft is now substantially out of date (Field 5, "search not yet executed," is already false). Status note added to the document; portal submission not pursued unless time permits in Phase 3.
- Title/abstract screening criteria (Issue #17, not yet drafted) will incorporate the proposal's IRR design: 15% random re-screen after a 2-week washout, intra-rater Cohen's κ, faculty adjudication for borderline cases — distinct from the existing extraction-stage 2-reviewer/5-paper-pilot protocol in `docs/osf/preregistration_draft.md` Section 7, which remains for extraction.
- Supplementary search/provenance plan (Google Scholar citation tracing of included studies plus grey-lit/preprint discovery via arXiv/SSRN; Elicit semantic search per RQ with logged queries/dates/counts; Rayyan for screening/dedup with provenance tracking per included study) to be documented in the protocol docs.

**Alternatives considered:**
- Run both reviews — cross-domain systematic review as a separate, longer-horizon project; EM scoping review as the graded 8-week deliverable. Rejected for now: maintaining two diverging protocols, search strings, and extraction schemas in parallel is not sustainable for a single reviewer in 8 weeks. The cross-domain framing and the validated PubMed 9,672-hit corpus remain in git history and can be revived in a later semester — the proposal explicitly frames this review as "scaffolding" for that work.
- Keep the 6-hypothesis confirmatory framing as the primary analysis and add EM framing on top. Rejected: does not satisfy the proposal's required JBI/PRISMA-ScR narrative-synthesis methodology, and several hypotheses (H4, H6) were already at risk of underpowered cells even in the larger cross-domain corpus — an EM-narrowed corpus would make this worse.
- Keep CINAHL and the 5-database scope. Rejected for the primary search — the proposal specifies 4 databases, and CINAHL's nursing/allied-health focus was more relevant to the broader population/context scope of the cross-domain review. May revisit as a sensitivity check if Phase 3 has spare time.

**Impact:** Files rewritten/updated as part of this pivot: `docs/protocol/inclusion_boundary.md` (rewritten, v2 EM-only), `docs/protocol/search_string_pubmed_v1.md` (Concept C addition + re-test, 234/213 hits), `data/extraction/schema_v1.csv` (v1.3, 10 new columns), `docs/osf/preregistration_draft.md` (rewritten v2 — RQ1-RQ3, eligibility, JBI/PRISMA-ScR methodology, H1-H6/QR repositioned as supplementary), `docs/osf/prospero_draft.md` (status note added documenting deprioritisation), `docs/protocol/screening_criteria.md` (new — Issue #17, T/A exclusion taxonomy + 15%-re-screen/intra-rater-kappa/faculty-adjudication IRR design), `docs/protocol/supplementary_search_plan.md` (new — Issue #23, Rayyan/Elicit/Google Scholar/provenance plan), `data/screening/prisma_counts.csv` (EM-narrowed v2 row added; T/A and full-text E1 exclusion rows annotated with pointers to the new screening-criteria taxonomy). All pivot deliverables identified in this entry are now complete.

**Remaining follow-on work (tracked separately, not blocking the pivot itself):** `data/screening/prisma_counts.csv` will need a fresh row set once the EM-narrowed search strings are executed and exported across all 4 databases — the current PubMed=9,672 row reflects the superseded cross-domain string. The A+C (234) vs A+B+C (213) PubMed string choice still needs to be finalised and logged (see `docs/protocol/search_string_pubmed_v1.md` Next Steps). Embase/IEEE/ACM translations (Issue #22) need Concept C added and re-derivation from the finalised PubMed v2 string. PMID 38142755 still needs to be tagged `retracted-excluded` in Zotero.

**Defense if challenged:** "This is not scope creep in a new direction — it is a return to the originally approved, graded proposal after an exploratory phase that (productively) over-built several constructs beyond what the proposal specified. Rather than discard that work, the more rigorous trust-calibration/plausibility distinction and 4-dimension ecological validity rubric are retained and applied as upgrades to the EM-only corpus the proposal specifies. The pivot is driven by a realistic 8-week single-reviewer capacity assessment against the grading rubric — particularly the 25%-weighted Analysis & Synthesis criterion, which rewards argument over hypothesis-test reporting — and by the timeliness of the regulatory-readiness framing (EU AI Act Article 13 is a 2024 regulation), which gives the narrower EM scope a stronger publication hook than the broader cross-domain framing had."

---

## 2026-06-10 — EM-narrowed v2 PubMed string finalized as A+B+C; date range extended to "2015 through search-execution date"

**Decision:** Two open items from the EM-pivot's `search_string_pubmed_v1.md` Next Steps were resolved:
1. **A+B+C** (not A+C) is adopted as the final v2 EM-narrowed structure, retaining Concept B for consistency with the cross-domain string's validated two-concept design.
2. The date range is extended from the proposal's fixed **2015/01/01–2024/12/31** to **2015/01/01 through the search-execution date** (a rolling "to present" window), executed as a single search rather than splitting into a 2015-2024 main search plus a deferred 2025+ update.

**Investigation (PubMed, A+B+C, English, live E-utilities, run 2026-06-10):**

| Period | Hits |
|---|---|
| 2015-2024 (proposal's registered window) | 213 |
| 2025 | 139 |
| 2026 Jan 1 - Jun 10 (partial year) | 171 |
| 2015-2026/06/10 (full extension to "now") | 497 (+133%) |

A spot-check of three 2026-dated PMIDs (42266581, 42260815, 42257858) confirmed genuinely recent epub/pubdate values (May-June 2026), not forward-dated placeholders.

**Relationship to the 2026-06-09 decision ("Date range kept at 2015-2024; 2025+ deferred to a planned pre-submission search update"):** That entry considered and rejected extending the *cross-domain* (Concept A+B, 9,672-hit) search to "now" (22,406 hits, +131%), for two reasons specific to that moment: (1) the cross-domain string had already been executed and exported on 2026-06-07 — extending would mean re-pulling 2.3x the records (~56 efetch batches) under a 2-day deadline; (2) a partial mid-2026 pull would need re-verification later regardless, due to Epub-ahead-of-print date instability for very recent records.

Neither reason transfers cleanly to the EM-narrowed v2 string:
- **No sunk export to preserve.** The EM-narrowed string has not yet been formally executed/exported under either date range — "extend now" and "extend later" both mean a *first* execution, not a re-pull. There is no 2.3x-rework penalty.
- **The corpus-size jump is much smaller in absolute terms.** 213 -> 497 (+284 records) is a manageable addition for single-reviewer T/A screening (`docs/protocol/screening_criteria.md`), unlike 9,672 -> 22,406 (+12,734).
- **The Epub-ahead-of-print instability concern is real but unavoidable either way.** Any search executed "close to now" — whether its lower bound is 2015 or 2025 — will include very-recent records whose `Date - Publication` field could be reclassified before formal execution. This is not a reason to exclude 2025-2026 from the *initial* search; it is a reason to re-run the finalized query (with the date range's upper bound set to the actual execution date) at execution time rather than relying on this 2026-06-10 design-time snapshot.

The 2026-06-09 entry's core methodological point — run the search close to submission to capture the most complete, stable corpus — is honored here too: extending the *initial* execution's window to "now" means the corpus is as current as possible at first execution, and the Phase 3 "search update" becomes a small top-up (records published/indexed between initial execution and submission) rather than an ~18-month catch-up pass covering more than half the eligible literature.

**Rationale:**
1. At the original (213-hit) window, the most recent 18 months (2025 + partial 2026 = 310 records) alone exceed the entire 2015-2024 corpus (213) — deferring this majority of the eligible literature to a lighter Phase-3 pass would be inconsistent with how the 2015-2024 corpus is screened, and is especially awkward given RQ3's regulatory-readiness framing (FDA AI/ML guidance and EU AI Act Article 13 are themselves recent; the most relevant evidence is likely concentrated in the most recent literature).
2. A+B+C retained over A+C (213 vs. 234 at 2015-2024): Concept B was already precision-tuned and recall-validated as part of the cross-domain string (2026-06-07 entry); keeping it preserves that validated design rather than introducing an untested 2-concept structure for the EM-narrowed corpus. The 21-record difference is within the tolerance of the T/A-stage sensitivity-favouring rule (`docs/protocol/screening_criteria.md` Section 3).

**Alternatives considered:**
- Apply the 2026-06-09 decision unchanged (keep 2015-2024 + plan a January-2025-onward update) — rejected: as argued above, the rationale that justified deferral for the cross-domain string (sunk export, 2.3x rework, 2-day deadline) does not apply to a string that has not been executed yet; deferring would mean over half the eligible EM-narrowed corpus is screened under a different, later, lighter-touch process.
- A+C (234 hits, the EM-pivot entry's original recommendation) instead of A+B+C (213 hits) — superseded by user decision (2026-06-10): A+B+C retains the validated Concept B and is adopted as the final structure.

**Impact:** `docs/protocol/search_string_pubmed_v1.md` updated: new "Date Range Decision" section with the table above, A+B+C promoted to "FINAL" (A+C retained as a documented rejected alternative), Next Steps renumbered. `data/screening/prisma_counts.csv` EM-narrowed PubMed row updated to A+B+C / extended range (497, design-time snapshot, pending formal execution). `docs/osf/preregistration_draft.md` Section 3 (Publication period) and Section 10 (Phase 3 timeline) updated to replace "2015-2024 + January 2025 update" with "2015 through search-execution date + small pre-submission top-up". Embase/IEEE/ACM translations (Issue #22) re-derived with Concept C added and restructured to A+B+C with the extended date range.

**Defense if challenged:** "The 2025-2026 surge finding from 2026-06-09 (cross-domain string) recurs at EM-narrowed scale: the most recent 18 months contain more eligible-looking records (310) than the entire prior decade (213). Unlike the cross-domain case, the EM-narrowed string had not yet been executed, so extending its date range to 'now' is a first-execution design choice, not a costly re-pull — and it keeps the bulk of the most-recent, most regulation-relevant literature in the same screening process as the rest of the corpus, with only a small top-up search needed before submission."

---

## 2026-06-11 — EM-specific recall benchmark validates A+B+C v2 FINAL string (6/8); one term-list gap documented, not remediated

**Decision:** The EM-narrowed A+B+C v2 FINAL PubMed string (`docs/protocol/search_string_pubmed_v1.md`, 213 hits 2015-2024 / 497 hits 2015-2026/06/11) is **validated** against a new EM-specific recall benchmark and **remains unchanged**. Next Steps item 9 is complete.

**Investigation:** The cross-domain benchmark used to validate the original Concept A/B string (Cao/Kunaprayoon/Ren, Tosun, Kumar, Gu — Revision note 3, 2026-06-07) does not transfer to the EM-narrowed scope (none of the four pass `inclusion_boundary.md` v2 Gate 1). `references/bib/foundational.bib` was checked and ruled out (general XAI-theory papers only). A new benchmark was assembled via an independent PubMed query using a deliberately *broader* term set than Concept A (bare `"feature importance"[tiab]`, `"explainable"[tiab]`, `"interpretable"[tiab]`, etc.) ANDed with EM/triage/disposition terms (653 hits); the top 30 were screened for clinical-XAI relevance, yielding 8 candidates checked against the live A+B+C idlist (497 PMIDs):

| PMID | Retrieved? | Gate 1 (abstract-level) | Notes |
|---|---|---|---|
| 38708185 | Yes | Pass (acuity/triage scoring) | via "interpretable machine learning" |
| 38102476 | Yes | Pass (risk stratification at triage) | via "SHAP" |
| 39176941 | **No** | Pass (disposition outcome) | Concept A = 0 — "feature importance" only |
| 40242564 | Yes | **Fail** (CT-scan-ordering decision) | correct retrieval, Gate-1 exclusion |
| 37578440 | **No** | Pass (admission/disposition) | Concept A = 0 — "permutation feature importance" only |
| 36634916 | Yes | Pass (admission prediction) | via "SHAP" — author-keyword (OT) field, not visible in abstract |
| 39176843 | Yes | **Fail** (length-of-stay = operational) | correct retrieval, Gate-1 exclusion |
| 40102847 | Yes | **Fail** (wait-time = operational) | correct retrieval, Gate-1 exclusion |

**Recall: 6/8 (75%).** Per-concept diagnosis (Concept A/B/C tested individually AND'd with `[uid]`) confirmed both misses are isolated entirely to Concept A (B=1, C=1 for both) — root cause: Concept A has no bare "feature importance"[tiab] term (removed in Revision note 3, 2026-06-07, specifically for over-broadening — it inflated Concept A alone to 70,946 hits). Of the two misses, PMID 39176941 used "feature importance" for exploratory feature selection only (plausibly fails Gate 2/3 regardless); PMID 37578440 used "permutation feature importance" — a recognized model-agnostic feature-attribution technique, and the more plausible Gate-2 pass of the two, but unrecoverable by this string.

A secondary finding: PMID 36634916 was retrieved despite no Concept A term appearing in its visible title/abstract — diagnosis traced this to `"SHAP"[tiab]` matching the MEDLINE "Other Term" (author-keyword) field (`OT - SHAP`), confirming PubMed's `[tiab]`/"Title/Abstract" search extends to author keywords. A third finding: 3/8 candidates (40242564, 39176843, 40102847) are correctly retrieved by A+B+C but fail Gate 1 of `inclusion_boundary.md` v2 (CT-scan-ordering and two operational/throughput models) — confirming the string is appropriately recall-oriented relative to the inclusion boundary, with screening doing the precision work as designed.

**Rationale for not remediating the "feature importance" gap:** Adding a bare `"feature importance"[tiab]` term to Concept A would risk reproducing the exact over-broadening Revision note 3 removed it to avoid — "feature importance" is reported in the large majority of tabular-ML papers regardless of any XAI framing. Against a confirmed cost of 1-2 records out of an EM-narrowed corpus of 497, re-opening a string already finalized and live-verified (213/497 hits) for a precision risk of this magnitude is not justified.

**Alternatives considered:**
- Add `"feature importance"[tiab]` (or a narrower variant such as `"permutation feature importance"[tiab]`) back to Concept A. Rejected: even the narrower "permutation feature importance" phrasing risks non-trivial over-broadening (it is a standard reporting phrase in any ML paper using scikit-learn's `permutation_importance` or similar, regardless of XAI framing) for a benefit of at most 1 record in this benchmark; and the string is already FINAL with a live-verified hit count.
- Treat the 2 misses as disqualifying and re-open the A+C vs. A+B+C / term-list decisions. Rejected: per-concept diagnosis shows the misses are isolated to a single, well-understood, previously-documented term-list trade-off (Known Limitations item 2, Revision note 3) — not a structural flaw in the A+B+C design.

**Impact:** `docs/protocol/search_string_pubmed_v1.md` updated: new "EM-Specific Recall Benchmark (2026-06-11)" section (methodology, 8-candidate table, 4 findings, decision); new Known Limitations item 8 ("feature importance"/"permutation feature importance" gap, with citation-chase mitigation at full-text screening); Next Steps item 9 marked done; Version History updated (new "v2 — recall-benchmarked" row); status line updated. No changes to the search string itself, hit counts, or `data/screening/prisma_counts.csv`.

**Defense if challenged:** "An independently-assembled 8-paper EM-XAI benchmark — using a deliberately broader candidate-finding query than the search string itself — shows 75% recall, with both misses traced via per-concept diagnosis to a single, previously-documented Concept A trade-off (the same 'feature importance' over-broadening that Revision note 3 removed on 2026-06-07 after it inflated Concept A alone to 70,946 hits). One of the two misses likely wouldn't pass Gate 2/3 regardless; the other is a single-record cost against a corpus of 497. The benchmark also surfaced a recall *strength* (author-keyword indexing under [tiab]) and confirmed the string's sensitivity-favouring design works as intended (3/8 candidates correctly retrieved despite failing the inclusion boundary's Gate 1). Re-opening a finalized, live-verified string for a 1-2 record gain is not warranted; the gap is documented and a citation-chase mitigation is specified for full-text screening."

---

## 2026-06-10 (addendum, logged 2026-06-11) — PubMed search formally executed (497 records)

**Decision/Event:** The A+B+C v2 FINAL PubMed string was formally executed on 2026-06-10 with date range 2015/01/01–2026/06/10 (English). Returned **497 records**, exactly matching the live-verified design-time snapshot from the same date. Raw export saved as `data/searches/pubmed-explainabl-set.nbib`.

**Impact:** `data/screening/prisma_counts.csv` PubMed Identification row updated from "DRAFT — not yet formally executed" to the formal count (497), pointing at the export file. `docs/protocol/search_string_pubmed_v1.md` status line, Full Combined String section, Date Range Decision note, Next Steps items 10–11, and Version History updated to record the execution.

**Remaining for Next Steps item 10:** Embase, IEEE Xplore, and ACM Digital Library searches still need to be formally executed, using the same 2026/06/10 date-range upper bound for consistency, with `prisma_counts.csv` updated per database as each is completed.

---

## 2026-06-18 — IEEE Xplore search formally executed (161 records); 10-wildcard Command Search cap discovered and fixed

**Decision/Event:** The A+B+C v2 IEEE Xplore string (`docs/protocol/search_string_ieee_v1.md`) was run against live Command Search on 2026-06-18 and rejected with the error "Limit the total number of wildcards to 10" — the original translation carried 22 wildcarded (`*`) terms (7 in Concept A, 12 in Concept B, 3 in Concept C), more than double IEEE Xplore's per-query cap.

**Fix:** 16 of the 22 wildcarded terms have small, predictable suffix sets (2-3 word forms, e.g. `"explainable model*"` → `"explainable model" OR "explainable models"`) and were manually enumerated as explicit `OR` clauses — no recall loss, since the variant sets are exhaustively known. The remaining 6 — single-word stems with unpredictable/numerous suffix forms (`computer-aided diagnos*`, `computer aided diagnos*`, `radiolog*`, `patholog*`, `nurse*`, `hospital*`) — kept the wildcard, since manually enumerating every plausible form (e.g. radiology/radiologist/radiologists/radiological) would itself risk missing a variant. This reduced the query to 6 wildcards, under the cap.

**Result:** the wildcard-limit-compliant string was run live 2026-06-18, date range 2015–2026/06/18, Command Search ("Full Text & Metadata" scope, Option 1) — **161 records**. Raw export saved as `data/searches/ieee_export_2026-06-18.csv`.

**Impact:** `docs/protocol/search_string_ieee_v1.md` updated: new "Wildcard-Limit Fix (2026-06-18)" section with the corrected string and rationale; Known Limitations item 7 added (10-wildcard cap, also a risk for the untested Option 2); Next Steps items 1, 3, 4 marked done; Version History updated. `data/screening/prisma_counts.csv` IEEE Xplore Identification row updated (161, pointing at the raw export).

**Remaining for Next Steps item 10 (PubMed protocol doc):** Embase and ACM Digital Library searches still need to be formally executed. Both translation docs (`search_string_embase_v1.md`, `search_string_acm_v1.md`) use the same wildcard-truncation pattern as the original IEEE draft — check each platform's wildcard/syntax limits before running, in case a similar fix is needed.

---

## 2026-06-18 — Wildcard-limit fix pre-applied to Embase and ACM Digital Library strings (neither yet run live)

**Decision:** Rather than wait for Embase.com and ACM DL to reject the original 22-wildcard translations the way IEEE Xplore did (entry immediately above), the same reduction was pre-emptively applied to both drafts before their first live run: 16 of 22 wildcarded terms enumerated as explicit word-form `OR` clauses, retaining the wildcard only on the 6 single-word stems with unpredictable suffix forms (`computer-aided diagnos*`, `computer aided diagnos*`, `radiolog*`, `patholog*`, `nurse*`, `hospital*`).

**Embase-specific note:** the fix applies cleanly — each concept block is a single `:ti,ab,kw`-tagged OR-list, so the wildcard count is 6 in the full combined string, same as the corrected IEEE string. Embase.com's actual wildcard limit (if any) remains unconfirmed.

**ACM-specific note — multiplier risk identified:** ACM's combined string nests each concept block inside three field brackets (`[Title: (...)] OR [Abstract: (...)] OR [Keyword: (...)]`), so Concept B's 6 retained wildcards are repeated once per field — **18 wildcard occurrences in the full combined string, not 6**. If ACM DL enforces a cap counted across the whole query (rather than per bracket), this string could still be rejected. `docs/protocol/search_string_acm_v1.md` Next Steps now recommend building the query incrementally (one field/concept at a time via "View Query Syntax") rather than pasting the full combined string on the first attempt, and dropping `nurse*`/`hospital*` to bare non-wildcard forms first if a wildcard error appears (cheapest precision loss of the 6).

---

## 2026-06-22 — ACM Digital Library execution paused (0-result syntax failure); proceeding to Embase

**Decision/Event:** Attempted to run the wildcard-fixed ACM string live at dl.acm.org/search/advanced — the full bracket-nested combined string returned **0 results**. Diagnosed via minimal fragments: `[Title: "machine learning"]` (single bracketed term, no OR) and `[Title: "machine learning"] OR [Title: "deep learning"]` (OR across two brackets) both *also* returned 0, despite "machine learning" being a near-certain high-volume ACM title term. This rules out a translation/term problem and points to either (a) the hand-typed bracket syntax not being valid raw input for that search box at all (it may be a UI-only display format for queries built through the Advanced Search form, not literal paste-able syntax), or (b) a more basic access/field-name issue. Recommended next diagnostic (not yet run): build a single-field/single-term search through the Advanced Search **form** (dropdown + text box, not the raw query box) to get ACM to generate its own correct syntax, rather than continuing to guess.

**Decision:** Pause ACM execution rather than continue guessing syntax variants. **This is a deferral, not a drop** — ACM is one of the 4 primary databases named in the OSF pre-registration (`docs/osf/preregistration_draft.md` Section 4: PubMed/Embase/IEEE/ACM) and is flagged in its own protocol doc as the most important of the four for recall validation (Kumar et al./Gu et al. benchmarks) — dropping it would require amending the registration. Proceeding to execute Embase next (PubMed and IEEE are already done) while the ACM syntax issue remains open.

**Impact:** No file changes yet to `search_string_acm_v1.md` Status line (still DRAFT/UNTESTED) — leaving it as-is since nothing about the string's content changed, only the open question of correct platform syntax. `prisma_counts.csv` ACM row remains blank. Revisit ACM once Embase is executed and logged.

---

## 2026-06-22 — Embase dropped from primary search: no institutional access

**Decision/Event:** Before executing the Embase string, confirmed institutional access. UNO (the reviewer's home institution) does not subscribe to Embase. UNMC (University of Nebraska Medical Center) does, but the reviewer is a UNO student with no enrollment, affiliation, joint program, or other authorized path to UNMC's license, and no librarian-mediated/interlibrary search route was available within the Phase 1 timeline. Considered and rejected two alternatives: (a) substituting an accessible database UNO does subscribe to (e.g. Scopus, Web of Science) in Embase's slot — rejected for now in favor of (b) simply dropping to 3 primary databases and documenting the gap, rather than introducing a new untranslated/unvalidated search string under time pressure.

**Decision:** Reduce primary database scope from 4 to **3: PubMed/MEDLINE, IEEE Xplore, ACM Digital Library**. Embase is logged as a documented protocol deviation, not a silent drop — to be reported as a limitation in the manuscript's methods/limitations section (loss of Emtree-indexed and conference-abstract-heavy coverage relative to MEDLINE/IEEE/ACM).

**Impact:** `docs/osf/preregistration_draft.md` Section 4 updated (deviation note + new "Draft v2.2" Version History row); `docs/protocol/search_string_embase_v1.md` status line updated to reflect the string is retained for the audit trail but will not be executed. `data/screening/prisma_counts.csv` Embase Identification row updated from blank to explicitly "N/A — dropped" with the access-constraint reason, rather than left blank/ambiguous.

**Remaining:** ACM Digital Library execution still open (syntax issue, see entry above). Once resolved, primary search Identification will be complete across the 3 databases (PubMed: 497, IEEE: 161, ACM: pending).

---

## 2026-06-22 — ACM Digital Library executed via OpenAlex API (methodology substitution; 1 record)

**Decision/Event:** Continued diagnosing the 0-result failure of ACM's native Advanced Search bracket syntax (entry above) with two minimal control-term fragments: `[Title: "machine learning"]` (single bracketed term) and `[Title: "machine learning"] OR [Title: "deep learning"]` (OR across two brackets). **Both returned 0 results**, despite "machine learning" being a near-certain high-volume ACM title term. This ruled out a translation/term-list problem and pointed to either (a) the bracket notation being a UI-only display format for queries built through ACM's form-based Advanced Search builder, not literal paste-able syntax, or (b) a more basic access issue. After 3 failed attempts, further guessing at ACM's native syntax was abandoned.

**Substitution:** ACM Digital Library has no official public search API (unlike PubMed's E-utilities or IEEE Xplore's Metadata API). Used the **OpenAlex API** (api.openalex.org) instead — a free, public scholarly index covering ACM's catalog — restricted to ACM as publisher via its OpenAlex ID (`P4310319798`, confirmed via the `/publishers` lookup endpoint, not guessed). This is a different system than ACM's own search engine (OpenAlex indexes metadata/abstracts via Crossref-deposited data), so it is logged as a documented methodology substitution rather than presented as equivalent to the originally planned native search.

**Verification before trusting the result:** confirmed boolean OR (pipe-separated), AND-across-concepts, wildcard truncation (via the unstemmed `.search.exact` field), year-range, and language filters each work correctly via small live test queries before assembling the full A+B+C string. Checked abstract coverage for the searched corpus: 63,606/64,974 (97.9%) of ACM works (2015-2026) have an indexed abstract — low but non-zero recall risk from the ~2% without one.

**Result:** **1 record** (DOI 10.1145/3453166, "Triage of 2D Mammographic Images Using Multi-view Multi-task Convolutional Neural Networks," 2021), using the same wildcard-fixed term lists from `docs/protocol/search_string_acm_v1.md`, 2015-2026, English. Diagnostic breakdown: Concept A alone (any ACM paper) = 773; Concept C alone = 32; A+C = 1; A+B+C = 1 — Concept C (EM-specific terms) is the binding constraint, not Concept B, consistent with the protocol doc's own prediction that ACM's CS/HCI-heavy corpus might yield "a plausible and informative null result" once EM-narrowed. The single hit is a radiology/mammography image-triage paper, not an ED patient-disposition paper — very likely to fail Gate 1 of the EM inclusion boundary at full-text screening, meaning ACM's practical contribution to the final included set may be zero even though 1 record counts toward PRISMA Identification.

**Impact:** `docs/protocol/search_string_acm_v1.md` updated with a full "Methodology Substitution (2026-06-22)" section (diagnostic fragments, OpenAlex query, verification steps, result, diagnostic breakdown), status line, Next Steps, and Version History. `docs/osf/preregistration_draft.md` Section 4 and Version History updated (Draft v2.2) to log this as a second documented protocol deviation alongside the Embase drop. `data/screening/prisma_counts.csv` ACM row updated to 1, pointing at the raw export `data/searches/acm_openalex_2026-06-22_1.json`.

**Primary search Identification is now complete across all 3 in-scope databases: PubMed (497), IEEE Xplore (161), ACM Digital Library (1) = 659 records before deduplication.** Embase remains formally out of scope (no institutional access). Next: deduplication in Rayyan, then title/abstract screening.

---

## 2026-06-26 — Rayyan import format fix; deduplication run (659 -> 650); stale retraction-QC count flagged

**Format fix:** Rayyan's import does not accept CSV. `data/searches/ieee_export_2026-06-18.csv` (161 records) was converted to RIS (`ieee_export_2026-06-18.ris`) via a small Node script (RFC4180-aware CSV parser; maps Document Title/Authors/Publication Title/Abstract/DOI/Author Keywords etc. to standard RIS tags). Verified 1:1 record conversion (161 `TY`/`ER` pairs in, 161 records out) before upload. The original CSV is retained in `data/searches/` for the audit trail; the `.ris` file is what was actually imported into Rayyan.

**Import mistake caught and corrected:** first Rayyan import reported 9,834 articles, not the expected 659. Diagnosed via arithmetic: 9,672 + 161 + 1 = 9,834 — the superseded cross-domain PubMed export (`pubmed_2026-06-07_v1-rev3_9672.nbib`) had been uploaded instead of the correct EM-narrowed one (`pubmed-explainabl-set.nbib`, 497 records), the two files having similar names in the same folder. The bad batch was deleted and re-uploaded with the correct file; total confirmed at 659 before dedup.

**Deduplication:** run in Rayyan 2026-06-26 across the merged `source:pubmed` (497) + `source:ieee` (161) + `source:acm` (1) corpus. **659 -> 650 records (9 duplicates merged)**, with multi-source labels preserved on surviving merged records per `docs/protocol/supplementary_search_plan.md`.

**Stale data caught:** `data/screening/prisma_counts.csv`'s existing "Retracted publications removed (pre-screening QC)" row (11) was computed 2026-06-08 against the now-superseded 9,672-record cross-domain export — it does not apply to the current 497/650-record EM-narrowed corpus and must not be subtracted from 650. Flagged in `prisma_counts.csv` as needing re-verification rather than silently reusing or silently dropping the row.

**Impact:** `data/screening/prisma_counts.csv` updated: Total records identified (659), Duplicates removed before screening (9), Records after deduplication (650, pending the retraction-QC re-check). Retraction QC row marked stale/needs re-verification rather than given a number.

**Next:** re-run retracted-publication QC against the current 650-record corpus (same MEDLINE RIN/PT-Retracted-Publication method as the 2026-06-08 check, applied to the right corpus this time), then begin title/abstract screening per `docs/protocol/screening_criteria.md` and `docs/protocol/inclusion_boundary.md` v2.

---

## 2026-06-26 (same day) — Retraction QC re-run on current corpus: 0 retracted records (corrects stale 11)

**Decision/Event:** Re-ran the retracted-publication pre-screening QC against `data/searches/pubmed-explainabl-set.nbib` (the current 497-record EM-narrowed PubMed export), using the same method as the 2026-06-08 check: scanned for `PT - Retracted Publication` (0/696 `PT` lines matched, across categories like Journal Article, Review, Validation Study, etc.), `RIN -` / Retraction-In field (0 matches), case-insensitive "retract" text search (0 matches), and `STAT` field anomalies (none — only standard MEDLINE/In-Process/PubMed-not-MEDLINE/Publisher values). Cross-checked that none of the original 11 retracted PMIDs from the 2026-06-08 check (against the superseded 9,672-record cross-domain export) appear in the current corpus at all, confirming they don't carry over.

**Result: 0 retracted publications** in the current 650-record (post-dedup) corpus. This corrects the stale "11" placeholder flagged in the entry above.

**Scope limitation noted:** this check only covers PubMed's structured retraction metadata (MEDLINE `PT`/`RIN` fields) — it does not cover the 161 IEEE or 1 ACM records, which have no equivalent structured retraction field. Given the small non-PubMed count, this is treated as a reasonable scope limit rather than a gap requiring further tooling, but is worth a one-line mention in the manuscript's limitations.

**Impact:** `data/screening/prisma_counts.csv` updated — "Retracted publications removed" row corrected from the stale placeholder to 0 (with full method documented), "Records after deduplication" confirmed at 650 (no further subtraction needed).

**Identification stage is now complete and clean: 650 records carried forward to title/abstract screening.**

---

## 2026-06-26 (same day) — Title/abstract screening started in Rayyan; criteria setup confirmed

**Event:** The TA-E1–TA-E5 exclusion codes and their inclusion-criteria counterparts (`docs/protocol/screening_criteria.md` Sections 3–4) were entered into Rayyan's "Screening criteria" panel. Confirmed Rayyan auto-numbers these in entry order as native criterion IDs `E1`–`E5` (exclusion) and `I1`–`I4` (inclusion) — verified directly against the panel, matching `TA-E1`→`E1` through `TA-E5`→`E5` exactly. No separate "Labels" feature exists in this Rayyan version; the `E#` criterion selected at decision time is the per-record exclusion-reason audit trail.

**Decision:** Rayyan's "Use with AI tools" toggle (AI-suggested Include/Exclude decisions) was found enabled by default on the inclusion criteria. Turned off before screening began, to keep screening fully manual — single reviewer, intra-rater IRR (15% re-screen, 2-week washout, Cohen's kappa per Section 5) — consistent with the registered protocol. No AI-assisted screening is in use; if this changes later, it needs its own decision-log entry and a protocol-deviation note (AI-assisted screening is reported differently under PRISMA-ScR than manual single-reviewer screening).

**Impact:** `docs/protocol/screening_criteria.md` Section 4a added documenting both the criterion-ID mapping and the AI-tools decision. **Title/abstract screening of the 650-record deduplicated corpus begins 2026-06-26** — this is the date the 2-week IRR washout period (Section 5) counts from; the 15% re-screen cannot start before 2026-07-10.

---

**Impact:** `docs/protocol/search_string_embase_v1.md` and `docs/protocol/search_string_acm_v1.md` updated in parallel — both concept blocks (A/B/C), Full Combined String sections, status lines, Known Limitations (new item: Embase #7, ACM #8), Next Steps, and Version History. Neither string has been run live yet; both remain DRAFT/UNTESTED pending the platform-confirmation and execution steps already listed in each doc's Next Steps.

---

## 2026-07-03 — Title/abstract screening of full 650-record corpus complete

**Decision/Event:** Title/abstract screening of the entire deduplicated 650-record corpus (begun 2026-06-26, per the entry above) is complete in Rayyan, single reviewer (ANIRBAN), blind mode on. Exported via Rayyan's "…" → Export menu as CSV (`data/screening/rayyan_ta_export_2026-07-03.csv`) and parsed: all 650 records have a recorded decision, none unscreened.

**Result:** Include: 40. Maybe/Borderline: 64 (9.8% of corpus — under the 10% threshold in `docs/protocol/screening_criteria.md` Section 6 that would flag a possible inclusion-boundary clarity issue). Exclude: 546. Records carried forward to full-text (Include + Maybe): 104.

**Gap identified:** the CSV export's `notes` field only encodes the Include/Exclude/Maybe decision (`RAYYAN-INCLUSION: {"ANIRBAN"=>"..."}`) — it does **not** include the per-record `TA-E1`–`TA-E5` reason code selected in Rayyan's criteria panel at decision time, despite that criterion selection being the intended reason-code audit trail per Section 4a. **Decision: deferred** — proceeding to full-text retrieval for the 104 carried-forward records without the reason-code breakdown for now; `data/screening/ta_exclusion_reasons.csv` remains unpopulated. If needed later for PRISMA reporting/manuscript, revisit whether Rayyan has a reasons-inclusive export mode or whether reason codes must be pulled per-record from the UI.

**Impact:** `data/screening/prisma_counts.csv` updated with real counts (Records screened: 650; excluded at T/A: 546; carried forward to full-text: 104), replacing the previously blank placeholder rows. Full per-record decisions saved to `data/screening/ta_decisions_2026-07-03.csv`. The 64 Maybe/Borderline records extracted to `data/screening/ta_borderline_list_2026-07-03.csv` as a faculty-adjudication worksheet (Section 6) — `gate_in_question`/`ambiguity_note` columns are blank for most records since this batch was screened directly in Rayyan (not via per-abstract gate-by-gate review), and `faculty_decision`/`faculty_rationale` columns are pending adjudication.

**Next:** (1) Faculty adjudication of the 64 Borderline records (Section 6) — decision and rationale to be logged here per record or in aggregate once complete. (2) IRR re-screen (Section 5): 15% random sample, blinded, re-screened no sooner than 2 weeks after each record's original decision — since primary screening ran 2026-06-26 to 2026-07-03, the safest single start date covering the whole sample is **2026-07-17** (2 weeks after the last screening date), though the protocol technically allows starting the earliest-screened portion from 2026-07-10. (3) Full-text retrieval for the 104 Include + adjudicated-Include Maybe records (Section 7).

---

## 2026-07-03 — Faculty adjudication of Borderline records delegated to sole reviewer (protocol deviation)

**Decision:** `docs/protocol/screening_criteria.md` Section 6 specifies that T/A Borderline records are "reviewed with the supervising faculty member," with the faculty adjudication decision and rationale logged here. The supervising faculty member is not available to review the 64 Borderline records individually and has verbally consented for the reviewer (Anirban) to evaluate and decide them alone, without a per-record faculty sign-off session.

**Rationale:** Faculty availability constraint; faculty has delegated adjudication authority to the sole reviewer rather than holding up Phase 1 progress.

**Alternatives considered:** (a) Wait for faculty availability before adjudicating — rejected, no timeline given and would block full-text retrieval indefinitely. (b) Async faculty review of the CSV without a live session — not what was agreed; faculty explicitly consented to the reviewer deciding, not to reviewing asynchronously.

**Impact:** The 64 Borderline records in `data/screening/ta_borderline_list_2026-07-03.csv` will be adjudicated by the sole reviewer, applying the full three-gate inclusion boundary (`docs/protocol/inclusion_boundary.md` v2) at the level of detail available in title/abstract, same as initial T/A screening. This converts what the registered protocol frames as a two-person check into a single-reviewer decision for this batch. The IRR re-screen (Section 5) remains the only reliability check on this reviewer's screening judgment overall; no additional second-opinion mechanism applies specifically to the Borderline batch.

**Defense if challenged:** Faculty supervisor explicitly delegated adjudication authority due to unavailability (verbal consent, 2026-07-03); this is disclosed here as a documented deviation from the registered Section 6 procedure, consistent with how other deviations in this log (Embase drop, ACM substitution) are handled — decided, justified, and logged rather than silently absorbed. Recommend a brief line in the manuscript's limitations noting Borderline-case adjudication was single-reviewer rather than two-person, consistent with the single-reviewer T/A screening design overall.

---

## 2026-07-03 — Gate 1 boundary clarification: in-ED treatment/procedural decisions are out of scope

**Decision:** During Borderline re-adjudication, encountered a record (rayyan-601300258, "AI for predicting shockable rhythm during CPR: In-hospital setting") where the population and setting are unambiguously ED, but the decision point — real-time shock/no-shock prediction during active resuscitation — does not fit any of Gate 1's three named categories (intake, acuity/triage scoring, immediate disposition). `docs/protocol/inclusion_boundary.md` did not previously address this case explicitly; its exclusion list covered EMS/inpatient/ICU/operational settings but not "occurs in the ED, but is a treatment/procedural decision rather than intake/triage/disposition."

**Clarification:** Gate 1's three categories are exhaustive, not illustrative — an ED-encounter decision point that is real-time treatment/procedural/management (resuscitation, medication dosing, imaging acquisition for diagnosis, physiologic monitoring during active care) fails Gate 1 even though it occurs during the ED encounter on an ED patient, because it is none of (a) intake, (b) acuity/triage scoring, or (c) immediate disposition.

**Rationale:** The original EM-pivot (2026-06-10) scoped Gate 1 specifically to intake/triage/disposition decision-support — the ED-flow/throughput decision points central to the review's motivating literature — not to the much broader universe of AI-assisted treatment/procedural decisions made during ED care (which is a distinct literature, e.g., resuscitation AI, point-of-care diagnostic AI). Extending Gate 1 to any decision merely "occurring in the ED" would substantially and unintentionally broaden scope beyond the registered protocol.

**Alternatives considered:** (a) Treat "occurs during active ED care" as sufficient for Gate 1 pass — rejected as inconsistent with the registered protocol's explicit three-category structure and likely scope creep. (b) Escalate every such case individually as Borderline without a general rule — rejected as inefficient and inconsistent given this is expected to recur (other resuscitation/procedural-AI records in the same corpus).

**Impact:** `docs/protocol/inclusion_boundary.md` updated to v2.1: new explicit Gate 1 exclusion bullet, a new edge-case table row (shockable-rhythm/CPR example), and a Version History entry. `C:\Users\anirb\.claude\projects\...\memory\project_screening_falsepositive_patterns.md` updated with this pattern for consistent application across the remaining Borderline batch. rayyan-601300258 itself is excluded under this clarification (Gate 1 fail) — see `data/screening/ta_borderline_list_2026-07-03.csv`.

**Defense if challenged:** This is a scope clarification grounded in the original EM-pivot's stated intent (ED-flow decision points: intake/triage/disposition), not a post-hoc narrowing to reach a preferred result — it was triggered by an actual boundary gap discovered during adjudication and is applied consistently to all subsequent records with the same shape, not selectively.

---

## 2026-07-03 — Gate 1 boundary clarification v2.2: patient-level predictions consumed administratively fail Gate 1

**Decision:** During Borderline re-adjudication, encountered a record (rayyan-601300617, "Predicting emergency department disposition using machine learning and large language models to support proactive capacity management") where the prediction target is individual-patient ED disposition (admit vs. discharge) — a Gate-1(c)-shaped outcome — but the paper explicitly and repeatedly frames the output as being acted on by "hospital decision-makers" for "proactive bed allocation, staffing coordination, and surge management," predicted "before physician evaluation," never framed as feeding back to the treating clinician's own decision for that patient.

**Clarification:** The decision-point-vs-population-origin test (already in `inclusion_boundary.md`) turns on *who acts on the output and toward what end*, not on the granularity of the prediction target. A patient-level prediction that is aggregated/routed into an administrative capacity-management workflow is an operational use — the same category as the existing "operational/administrative ED models" exclusion (crowding/throughput/staffing) — even though the underlying target variable (disposition) would pass Gate 1 if it were actually returned to the treating clinician.

**Rationale:** Without this clarification, any capacity-forecasting paper built on a per-patient ML model (a common and growing pattern — using individual predictions and rolling them up for bed/staffing planning) would pass Gate 1 on target-variable inspection alone, which would substantially and unintentionally broaden scope to include operational-research papers that happen to use patient-level features, contradicting the review's EM-pivot intent (ED-flow decision-support literature, not hospital operations research).

**Alternatives considered:** (a) Treat any patient-level disposition-shaped target as sufficient for Gate 1 pass regardless of stated use — rejected, scope creep into operations-research literature. (b) Escalate every such case individually — rejected as inefficient given this is expected to recur (capacity-forecasting-via-per-patient-ML is a common paper design).

**Impact:** `docs/protocol/inclusion_boundary.md` updated to v2.2: new explicit Gate 1 exclusion bullet, a new edge-case table row (ML+LLM ED disposition-for-capacity-management example), and a Version History entry. `project_screening_falsepositive_patterns.md` updated with this pattern. rayyan-601300617 itself is excluded under this clarification (Gate 1 fail).

**Defense if challenged:** Same grounding as the v2.1 clarification — this refines application of an already-registered test (decision-point-vs-population-origin) to a fact pattern the original protocol text didn't explicitly anticipate, rather than introducing a new criterion; applied prospectively and consistently, not to reach a preferred result on this specific record.

---

## 2026-07-03 (through 2026-07-06) — Borderline adjudication complete: all 64 records resolved

**Decision/Event:** Adjudication of the 64 T/A Maybe/Borderline records (delegated to the sole reviewer per the 2026-07-03 faculty-delegation entry above) is complete. Each record was assessed one at a time: the ta-screener subagent gave a gate-by-gate recommendation against `docs/protocol/inclusion_boundary.md`, and the reviewer made the final call. Full per-record rationale is in `data/screening/ta_borderline_list_2026-07-03.csv`.

**Result:**
- **Exclude: 40** — TA-E1 (wrong ED decision point/setting) 25, TA-E4 (wrong publication type/no empirical component) 7, TA-E2 (not an EM/ED clinical context) 5, TA-E3 (no XAI component) 2, TA-E5 (not an AI/ML study) 1.
- **Include / forward to full-text: 24** — 20 resolved to Include outright, 4 kept as genuine Borderline pending full-text confirmation on a specific narrow question (each flagged in the CSV's `faculty_rationale` column).

**Two protocol boundary clarifications emerged during this pass and were formalized in `docs/protocol/inclusion_boundary.md`** (both already logged in their own entries above, 2026-07-03): v2.1 (in-ED treatment/procedural/diagnostic decisions — CPR, test-ordering, diagnostic differentiation — are not intake/triage/disposition and fail Gate 1 even in an ED population) and v2.2 (patient-level predictions consumed administratively for capacity/staffing planning fail Gate 1 regardless of prediction-target granularity). These were applied retroactively and consistently across all subsequent records once identified, not selectively.

**Pattern observed across the batch:** a substantial share of the original bulk "Maybe" calls reversed cleanly to Exclude once walked gate-by-gate against the full protocol text — recurring shapes were: (1) ICU-admission-and-after decision points misread as ED-adjacent due to population origin (records with "emergency" in a combined ICU/EM department name, or ED-admitted cohorts followed into the ICU); (2) bare "triage" keyword matches in non-ED domains (dermatology) or non-triage senses (orthopedic operative/non-operative routing, diagnostic differentiation); (3) review/narrative-review/bibliometric/consensus-guideline papers with no underlying empirical model; (4) operational/administrative models (crowding, billing-code prediction, visit forecasting, capacity management) mistaken for patient-level decisions. This is consistent with the bulk T/A pass having been done at speed across the full 650-record corpus without per-record gate notes, versus this adjudication pass applying the full three-gate boundary explicitly to each ambiguous case.

**Impact:** `data/screening/prisma_counts.csv` Screening-stage rows updated to final counts: 586 excluded at T/A (546 bulk + 40 adjudicated), 64 carried forward to full-text (40 bulk Include + 24 adjudicated). `data/screening/ta_borderline_list_2026-07-03.csv` is the complete audit trail for this batch.

**Next:** (1) IRR 15% re-screen (Section 5 of `docs/protocol/screening_criteria.md`) — safest uniform start date 2026-07-17. (2) Full-text retrieval and screening for the 64 records carried forward (Section 7), applying the full inclusion boundary (now v2.2) decisively, including resolving the specific open questions flagged for the 4 records still marked genuinely Borderline and the ~8 Include-with-a-full-text-check-flag records.

---

## 2026-07-10 — Full-text screening pilot: Rule 7 added (E4 vs E1 for reviews)

**Decision/Event:** While screening the 10-paper full-text pilot (`docs/protocol/screening_fulltext_criteria.md` Section 6), record `rayyan-601300218` ("Interpretable Machine Learning for Emergency Department Triage: A Systematic Literature Review") exposed a gap in the exclusion-code priority rule. It is a systematic review, so it trivially fails Gates 1-3 (it doesn't itself deploy a clinical AI system, process individual patients, or involve a clinician in a decision loop, it discusses other papers that might). Applying the numeric tie-break rule literally ("lowest-numbered code wins when multiple reasons apply") would assign E1 (priority 1) over E4 (priority 4, wrong publication type), even though the paper is unambiguously and simply a review.

**Clarification:** Added Rule 7 to `docs/protocol/screening_fulltext_criteria.md` Section 5 (now v1.1): if a paper's Gate 1-3 failures stem solely from its being a review, editorial, commentary, protocol-only paper, or abstract-only submission, code E4, not E1, as an explicit exception to the numeric tie-break. E1 is reserved for primary empirical studies that fail on substantive domain, decision-point, or clinician-involvement grounds despite being an eligible study type. `rayyan-601300218` is coded E4 under this rule.

**Rationale:** Without this exception, E1 would win the tie-break for every review article that reaches full-text screening (since reviews definitionally fail the gates by not deploying anything), making E4 structurally unusable for its intended purpose of PRISMA-reportable wrong-publication-type accounting. The exception targets the specific case where gate failure is a consequence of format rather than a substantive finding about clinical domain fit.

**Alternatives considered:** (a) Keep the literal numeric tie-break with no exception, so E1 always wins, rejected because it makes E4 practically unreachable. (b) Defer the decision until more pilot cases accumulate, rejected because the pattern is expected to recur across the remaining ~54 records and a documented rule is needed before then.

**Impact:** `docs/protocol/screening_fulltext_criteria.md` updated to v1.1 (Rule 7 added, Version History updated). This is the second correction identified during the pilot's first 5 papers, the first being the earlier `rayyan-601300087` E3-to-E1 correction, a straightforward application of the existing numeric tie-break rather than a new rule. See `data/screening/fulltext_pilot_wave1_2026-07-10.csv` for the full per-paper record and gate-by-gate rationale.

---

## 2026-07-10 — Full-text screening pilot: sole reviewer confirmed, formal intra-rater IRR skipped

**Decision/Event:** The supervising faculty member, though busy and unavailable for active co-screening, confirmed (2026-07-10, verbal) that the reviewer may proceed solo through full-text screening and extraction, the same accommodation given for T/A borderline adjudication on 2026-07-03. Given summer-project timeline pressure, the reviewer cannot wait for the ~2-week washout period needed to make a genuine blind Wave 2 re-screen of the 10-paper pilot batch (`data/screening/fulltext_pilot_wave1_2026-07-10.csv`). A same-day or near-term re-screen would not be blind in any meaningful sense, since the detailed gate-by-gate rationale for each paper is still fresh from Wave 1, and any resulting kappa would be artificially inflated and would not constitute genuine evidence of reliability.

**Decision:** Formal intra-rater Cohen's kappa validation for the full-text screening pilot is skipped. The reviewer proceeds directly to full-text screening of the remaining ~54 records using the criteria as refined during Wave 1 (Rule 7 for E1-vs-E4 on reviews; the Gate 1 diagnostic-differentiation clarification applied to `rayyan-601300077` and `rayyan-601300067`, both consistent with the already-registered v2.1/v2.2 boundary rules, not new criteria). The per-paper gate-by-gate rationale already recorded for each of the 10 pilot papers stands as the audit trail in place of a kappa statistic.

**Rationale:** A same-day re-screen produces a number that looks like reliability evidence but isn't, since it measures memory of the just-completed Wave 1 pass rather than independent judgment. Skipping the kappa calculation and disclosing the gap honestly is more defensible than reporting an inflated kappa that wouldn't survive scrutiny. This mirrors the existing treatment of the T/A-stage sole-reviewer deviation and the Embase/ACM search deviations: documented, justified, and disclosed as a limitation, not silently absorbed or manufactured around.

**Alternatives considered:** (a) Proceed with an immediate Wave 2 anyway and report the resulting kappa, rejected as scientifically misleading. (b) Use a shortened but still-real washout (3-5 days), rejected given the reviewer's stated timeline constraint that screening cannot wait even that long. (c) Wait for the full ~2-week washout before starting full-corpus screening, rejected for the same timeline reason.

**Impact:** No IRR statistic will be reported for the full-text screening stage. This is a documented protocol deviation from the piloting design in `docs/protocol/screening_fulltext_criteria.md` Section 6 (which assumes two independent reviewers) and should be disclosed in the manuscript's Methods/Limitations section alongside the T/A-stage sole-reviewer note: "Full-text screening reliability was not formally validated via inter-rater or intra-rater kappa due to reviewer availability and timeline constraints; screening decisions and gate-by-gate rationale for all records are available in the study's data repository." The extraction-stage 5-paper pilot (Section 8 of the OSF preregistration) will face the same constraint and should be resolved the same way when it comes up, unless circumstances change.

**Next:** Begin full-text screening of the remaining ~54 records (the 10 pilot papers are done, all excluded). Continue applying Rule 7 and the Gate 1 diagnostic-differentiation clarification consistently. Continue chasing the 9 records still pending manual PDF retrieval in parallel; retrieval status doesn't block screening of records already in hand.

---

## 2026-07-13 — Full-text screening: first 5 of remaining 54 (058, 059, 060, 063, 066)

**Decision/Event:** Screened via `fulltext-screener` subagent, one paper per isolated call, against `docs/protocol/inclusion_boundary.md` v2.2 and `docs/protocol/screening_fulltext_criteria.md` v1.1.

- `rayyan-601300058` — Exclude, E4. Narrative literature survey of 25 articles; Table 2's trust/interpretability/accuracy scores are aggregated from the surveyed papers, not an original study. Abstract self-identifies as a survey.
- `rayyan-601300059` — Exclude, E4. Narrative overview of triage methods and CDSS/AI concepts; XAI discussed conceptually (Section V-E) only, never implemented; no dataset, no results section.
- `rayyan-601300060` — Exclude, E3. Reviewer initially disagreed with the subagent's F3 call and asked for the paper to be re-checked directly against the text rather than the subagent's summary. Re-extracted the PDF (Section IV.B "ML model Accountability") and confirmed: SHAP (Fig. 7) and LIME (Fig. 8) are applied and their outputs described, but never evaluated — no fidelity/consistency/stability proxy metric and no clinician assessment of the explanations; all reported "evaluation" language (AUC 91%, F1 70%, confusion matrix) refers to the underlying classifier, not the explanations. Reviewer accepted the E3 call after reviewing the extracted text directly. Gates 1-2 pass cleanly (ESI acuity prediction, individual-patient); Gate 3 passes weakly (aspirational clinician-in-loop language).
- `rayyan-601300063` — **Include.** Rule-extraction (te2rules) on a Gradient Boosting model, MIMIC-IV-ED, evaluated via fidelity (98.90% overall) and rule-quality proxy metrics (coverage, consistency, relative coverage) — all F1-F5 satisfied on computational-fidelity grounds alone, no clinician study, matching the precedent edge-case pattern (fidelity-only evaluation without a clinician study is sufficient for F3, per Rule 3). Uncertainty flagged: the paper never uses "disposition" or "acuity scoring" for its own model, self-describing as predicting "critical outcomes ... during ED triage" from triage-time variables — Gate 1(a)/(b) mapped by analogy to prior sepsis-early-warning/pediatric-febrile-infant precedent, not a direct terminology match. Reviewer did not challenge this mapping.
- `rayyan-601300066` — Exclude, E4. Self-labeled "Assessment Protocol"; the prospective clinician-comparison study is explicitly "scheduled," not yet conducted, no participants recruited, no results reported.

**Rationale:** `rayyan-601300060` is a useful confirming case for the E3 criterion under direct reviewer challenge: the subagent's original read held up against the primary text (SHAP/LIME are presented, not evaluated), reinforcing that "figure + narrative description only" is a stable E3 pattern even when pushed on.

**Impact:** `data/screening/fulltext_master_2026-07-06.csv` updated (`fulltext_screened`, `fulltext_decision` columns) for these 5 records. Running full-text tally so far: 10 pilot (0 Include, 10 Exclude) + 5 this batch (1 Include, 4 Exclude) = 15 screened, 1 Include, 14 Exclude, 49 remaining.

**Next:** Continue full-text screening of the remaining 49 records from `data/screening/fulltext_remaining_54_2026-07-10.csv`, same per-paper isolated `fulltext-screener` dispatch pattern.

---

## 2026-07-13 — Full-text screening: next 5 of remaining 54 (068, 073, 074, 076, 083)

**Decision/Event:** Screened via `fulltext-screener` subagent, one paper per isolated call, against `docs/protocol/inclusion_boundary.md` v2.2 and `docs/protocol/screening_fulltext_criteria.md` v1.1.

- `rayyan-601300068` — **Include.** TE2Rules global rule extraction (35 rules) from a 100-tree Gradient Boosting model predicting ED hospitalization (admit/discharge), MIMIC-IV-ED, fidelity 0.879 (positive fidelity 1.0, negative fidelity 0.785). Gates 1-3 pass; output framed for "ED practitioners," not administrators. Gate 2 flagged as the closest call (Concluding Remarks phrase "efficiently deploy hospitalization resources required" echoes operational/resource-planning language), but the v2.2 administrative-consumption exclusion pattern (`inclusion_boundary.md` edge-case table, ED crowding/throughput model with SHAP "for hospital administrators") requires an aggregate/administrator-consumed metric; this paper's target is a per-patient binary outcome explicitly consumed by clinicians, so Gate 2 confirmed pass on direct comparison against that table row.
- `rayyan-601300073` — Exclude, E3. SHAP applied to a multiclass (C1-C5) triage-level Random Forest/GB model; output is two class-specific SHAP plots (Fig. 2, Fig. 3) with narrative clinical-plausibility commentary only ("SHAP analysis confirms... clinically plausible... provides confidence"), no proxy metric, no clinician rating. Matches the canonical E3 pattern (ICU-mortality/SHAP-figure example in `screening_fulltext_criteria.md`).
- `rayyan-601300074` — Exclude, E3. SHAP applied to a stacking-ensemble in-hospital-mortality model (MIMIC-IV/MIMIC-IV-ED), presented as a global/local feature-importance figure (Fig. 2) with narrative discussion only; no fidelity/faithfulness metric, no human-participant evaluation, no deployment study. Gate 1 flagged as boundary-adjacent (no concrete admit/disposition action named, only generic "prioritization"/triage-augmentation language, similar to prior precedent `rayyan-601300131`), but immaterial to the final code since F3 fails unambiguously either way.
- `rayyan-601300076` — Exclude, E3. SHAP (TreeSHAP) applied to a Random Forest KTAS binary triage classifier; per-patient waterfall-plot explanations described and asserted as "clinically plausible," with a stated future-deployment recommendation (nurse-facing SHAP display) but no clinician evaluation actually conducted ("evaluated retrospectively and internally only; no external or temporal validation is performed"). No proxy metric computed on the SHAP outputs themselves.
- `rayyan-601300083` — **Include.** LIME applied to a CamemBERT-based NLP model predicting ED admission/discharge from French-language triage notes. F3 met via a minimal but genuine human-participant evaluation: a physician co-author reviewed LIME word-level explanations against clinical reasoning for two worked examples ("evaluation was conducted in collaboration with a physician who possesses domain expertise in emergency medicine"), distinguishing this from the author-only narrative pattern seen in `068`/`073`/`074`/`076` where no clinician touched the XAI output at all. This is consistent with Rule 4 ("include if the XAI output is part of any described clinician interaction") and F3's explicit "however minimal" standard, though flagged as the thinnest Include in the corpus so far (single co-author, no rating scale, two examples only).

**Rationale:** This batch sharpens the E3-vs-Include boundary at its thinnest point: three papers (`073`, `074`, `076`) all show the identical pattern of SHAP applied + narrated as "clinically plausible" with zero clinician participation, confirming E3 as a stable, recurring pattern rather than a one-off. `083` is the deliberate contrast case — the presence of even one clinician actually engaging with the explanation output (not just the authors asserting plausibility) is what tips F3 from fail to pass per the protocol's explicit "however minimal" language.

**Impact:** `data/screening/fulltext_master_2026-07-06.csv` updated (`fulltext_screened`, `fulltext_decision` columns) for these 5 records. Running full-text tally: 10 pilot (0 Include, 10 Exclude) + 10 remaining-54 screened so far (2 Include, 8 Exclude) = 20 screened, 2 Include, 18 Exclude, 44 remaining.

**Next:** Continue full-text screening of the remaining 44 records from `data/screening/fulltext_remaining_54_2026-07-10.csv`, same per-paper isolated `fulltext-screener` dispatch pattern.

---

## 2026-07-13 — Full-text screening: next batch of remaining 54 (086, 220, 228, 239, 248 requested; 220/239/248 blocked on PDF retrieval)

**Decision/Event:** User requested screening of 086, 220, 228, 239, 248. Checked `data/screening/fulltext_remaining_54_2026-07-10.csv` and confirmed on disk: `rayyan-601300220` (`pdf_retrieved="no"`), `rayyan-601300239` (`pdf_retrieved="no"`), and `rayyan-601300248` (`pdf_retrieved="no"`) have no PDF in `data/extraction/fulltext_pdfs/` — all three are part of the 9-record set still pending the professor's institutional-access retrieval (see `project_fulltext_screening_progress.md`, "9 still pending"). Screening deferred for these 3 until PDFs are retrieved. Only `rayyan-601300086` and `rayyan-601300228` had PDFs in hand and were screened via `fulltext-screener` subagent against `docs/protocol/inclusion_boundary.md` v2.2 and `docs/protocol/screening_fulltext_criteria.md` v1.1.

- `rayyan-601300086` — Exclude, E3. Hybrid GAN-Boosting (AdaBoost/XGBoost/CatBoost + GAN augmentation) urgent/non-urgent triage classifier; SHAP applied to all six model variants, presented only as feature-ranking figures (Figs. 5-10) with narrative discussion, no proxy metric, no clinician evaluation. Stated primary contribution is the hybrid-model architecture itself, not XAI, so MethodPaper exception does not apply. Matches the now well-established recurring E3 pattern (SHAP-as-decoration, no evaluation of the explanation).
- `rayyan-601300228` — Exclude, E4. Self-declared "scoping review" of prehospital (pre-ED-arrival) emergency care AI/ML, PRISMA flow over 106 included studies; explainable AI discussed only narratively as a future-direction topic in the Discussion, never applied or evaluated by the authors. Both a format failure (review, no embedded primary study) and a substantive scope failure (prehospital, not ED — excluded per `inclusion_boundary.md`'s explicit "pre-hospital/EMS" exclusion), correctly resolved to E4 under Rule 7 since the Gate 1-3 failures are inseparable from the review's aggregate-synthesis format (no single decision point/individual-patient/clinician-loop claim of its own).

**Rationale:** `086` is the fourth consecutive paper in this project's screening to reproduce the identical "SHAP applied, narrated as clinically-plausible-or-informative, never evaluated" pattern (following `073`, `074`, `076` in the prior batch), further reinforcing E3 as the dominant failure mode at this stage of the corpus rather than Gate 1-3 substantive failures. `228` reinforces the precedent-driven E4-under-Rule-7 pattern established by `rayyan-601300218` for review-format papers.

**Impact:** `data/screening/fulltext_master_2026-07-06.csv` updated for `086` and `228` (`fulltext_screened="yes"`). `220`, `239`, `248` remain `fulltext_screened="no"` pending retrieval, unchanged this session. Running full-text tally: 10 pilot (0 Include, 10 Exclude) + 12 remaining-54 screened so far (2 Include, 10 Exclude) = 22 screened, 2 Include, 20 Exclude, 42 remaining in queue (3 of the 42 additionally blocked on retrieval: 220, 239, 248).

**Next:** Continue full-text screening of records with PDFs already in hand from `data/screening/fulltext_remaining_54_2026-07-10.csv`; chase retrieval for the 9-record pending set (which includes 220, 239, 248) in parallel, not as a blocker.

---

## 2026-07-13 — Correction: full-text running-tally Include count was off by one

**Decision/Event:** While answering a user question about corpus size, verified the running tally directly against `data/screening/fulltext_master_2026-07-06.csv` (`grep -c '"Include"'` / `grep -c 'Exclude'`) rather than trusting the cumulative narrative counts reported in the two preceding entries. The narrative tallies had drifted: the entry above (and the one before it) reported "2 Include," but the master CSV shows 3 (`rayyan-601300063`, `rayyan-601300068`, `rayyan-601300083`). The undercount originated when `063`'s earlier Include (from the first batch of 5) was dropped while summing forward across batches.

**Correction:** Verified current true state directly from source: **22/64 full-text records screened, 3 Include, 19 Exclude, 42 remaining** (3 of the 42 — `220`, `239`, `248` — additionally blocked on PDF retrieval). No CSV data was wrong; only the narrative running-tally arithmetic in chat/decision-log summaries had drifted. Persistent memory (`project_fulltext_screening_progress.md`, `MEMORY.md`) corrected to match.

**Rationale:** Cumulative "add N to running total" arithmetic across many turns is error-prone and unverified; the master CSV is the single source of truth and should be re-tallied directly (not incremented narratively) whenever the count matters for a decision (e.g., estimating final corpus size).

**Impact:** No data changes. Going forward, report full-text tallies by re-querying `fulltext_master_2026-07-06.csv` directly rather than incrementing a remembered running total.

---

## 2026-07-13 — Full-text screening: next batch of remaining 54 (252, 262, 267, 269, 293, 326, 366, 391 requested; 262/267 blocked on PDF retrieval)

**Decision/Event:** User requested 252, 262, 267, 269, 293, 326, 366, 391. Confirmed via `fulltext_remaining_54_2026-07-10.csv` and disk that `rayyan-601300262` and `rayyan-601300267` have `pdf_retrieved="no"` with no file present — deferred, not yet screenable. The remaining 6 were screened via `fulltext-screener` subagent against `docs/protocol/inclusion_boundary.md` v2.2 and `docs/protocol/screening_fulltext_criteria.md` v1.1.

- `rayyan-601300252` — Exclude, E2. "SERP+" score (AutoScore-Imbalance framework), inherently interpretable additive point score, but interpretability is not this paper's stated primary contribution (stated contribution is class-imbalance correction) and is never deliberately evaluated — only a coefficients/points table (Table 3) reported, plus a passing narrative variable-count comparison. Both prongs of Rule 1 fail.
- `rayyan-601300269` — Exclude, E4. Self-declared systematic review (PROSPERO CRD42024604529, PRISMA flow, 60 included studies); XAI (SHAP/LIME) discussed only as a finding about the reviewed literature, not applied or evaluated by the authors. Clean Rule 7 case, same pattern as `rayyan-601300218`.
- `rayyan-601300293` — Exclude, E1. Hematologic biomarker (MDW) prognostic-characterization study for sepsis-associated poor outcomes; no ED intake/triage/disposition action described anywhere in the text (zero grep hits for disposition/discharge/triage/ESI/acuity), clinical decision support framed only as future aspiration. Diagnostic/prognostic-differentiation Gate 1 failure, same pattern as `rayyan-601300077`/`rayyan-601300067`/`rayyan-601300326` (below).
- `rayyan-601300326` — Exclude, E1. Sepsis diagnosis (present/absent per Sepsis-3 criteria) from biomarkers/vitals; zero grep hits for disposition/discharge/transfer, "triage" only appears in a reference-list citation. Same diagnostic-differentiation pattern as `293`. E1 outranks the also-present candidate E3 per the numeric tie-break; Rule 7 does not apply since this is a substantive Gate 1 failure, not a format-driven one.
- `rayyan-601300366` — **Include.** SHAP-based CDSS for ED unscheduled-revisit risk, tied to the ED discharge decision itself ("physician plans to admit... considers the level of service"-equivalent framing for discharge); per-patient SHAP dashboard built for and piloted with treating physicians, who rated the explanations' trustworthiness/clinical soundness in a small-scale survey. Structurally matches the boundary doc's own worked "ED-discharge readmission-risk model reviewed by ED physician at discharge" Include example.
- `rayyan-601300391` — **Include.** Original SERP score paper (Xie et al. 2021, JAMA Network Open) — the sibling/predecessor of `252`'s "SERP+". Unlike `252`, interpretability *is* explicitly the stated primary contribution here (title: "...Interpretable Machine Learning Triage Tool..."). F3 satisfied via a deliberate parsimony-plot sparsity analysis (performance vs. number of variables, explicitly used to select the parsimonious variable set), matching Rule 3's sparsity proxy-metric allowance and the boundary doc's precedent row for computational-fidelity-only evaluation of inherently interpretable models. Flagged as the closest call in this batch: the authors themselves describe deeper interpretability/usability evaluation (e.g., physician-perceived acceptability) as future work, which could be read as the parsimony plot being routine model-construction rather than a deliberate interpretability evaluation. Resolved in favor of Include per Rule 3's explicit "however minimal" standard for proxy metrics.

**Rationale:** `252`/`391` are a deliberate contrast pair worth recording for internal consistency: same underlying score family (SERP), same inherently-interpretable-model mechanism, but opposite F2/F3 outcomes because `391` frames interpretability as its primary contribution and includes a deliberate sparsity trade-off analysis, while `252`'s primary contribution is class-imbalance correction with no deliberate interpretability evaluation of its own. `293`/`326` reinforce the diagnostic/prognostic-differentiation Gate 1 exclusion pattern as recurring and stable across a third and fourth instance.

**Open follow-up:** a sibling paper to `391`, `rayyan-601300657` ("Integrating... SERP... with emergency department triage to better predict 30-Day mortality"), is still in the remaining-54 queue and should be screened with the same Rule 1/Rule 3 reasoning applied here for consistency when it comes up.

**Impact:** `data/screening/fulltext_master_2026-07-06.csv` updated for `252`, `269`, `293`, `326`, `366`, `391` (`fulltext_screened="yes"`). `262`, `267` remain `fulltext_screened="no"` pending retrieval. Running full-text tally (re-verified directly against the master CSV per the correction above): 10 pilot (0 Include, 10 Exclude) + 18 remaining-54 screened so far (5 Include, 13 Exclude) = 28 screened, 5 Include, 23 Exclude, 36 remaining in queue (5 of the 36 blocked on retrieval: 220, 239, 248, 262, 267).

**Next:** Continue full-text screening of records with PDFs already in hand from `data/screening/fulltext_remaining_54_2026-07-10.csv`; chase retrieval for the now-5-record pending set in parallel, not as a blocker.

---

## 2026-07-13 — Full-text screening: next batch of remaining 54 (418, 431, 432, 454, 489, 504, 516, 564)

**Decision/Event:** User requested 418, 431, 432, 454, 489, 504, 516, 564. All 8 had `pdf_retrieved="yes"` with files on disk — no retrieval gaps this batch. All 8 screened via `fulltext-screener` subagent against `docs/protocol/inclusion_boundary.md` v2.2 and `docs/protocol/screening_fulltext_criteria.md` v1.1. All 8 excluded (0 Include this batch).

- `rayyan-601300418` — Exclude, E1. Hematological-indicator (CBC/RDW/PDW/PLT) diagnostic classification of acute heart failure vs. healthy controls; cohort drawn from cardiology department (case/control design), not an ED intake/triage/disposition population — only incidental ED framing in the Introduction. Diagnostic-differentiation Gate 1 failure, same pattern as `077`/`067`/`293`/`326`; structurally identical to the same author group's prior AMI-from-bloodwork paper already used as the boundary doc's worked example.
- `rayyan-601300431` — Exclude, E4. Self-declared PRISMA systematic review of 20 hospital-admission-prediction studies (CHARMS extraction, PROBAST bias assessment); "interpretability" mentioned only twice as a passing remark about logistic regression in the reviewed literature, never applied or evaluated by the authors themselves. Clean Rule 7 case, same pattern as `218`/`269`.
- `rayyan-601300432` — Exclude, E1. "EDT-MCFEF" department/specialty-routing text classifier (Urology, dermatology, gynecology, etc. — not an acuity/ESI/CTAS scale, not admit/discharge/transfer); "triage" used loosely for department assignment. Also independently fails F2: claimed "interpretability" is asserted from the multi-channel architecture design alone, never operationalized (no SHAP/LIME/attention-weight extraction; the "case study" is qualitative error analysis, not a formal explanation method). E1 outranks the also-present E2 per the numeric tie-break (primary empirical study, not a Rule 7 format case).
- `rayyan-601300454` — Exclude, E1. In-hospital-cardiac-arrest prediction model explicitly framed around paramedic pre-hospital transport/hospital-selection decisions ("paramedics can use this process to reduce the retransfer of emergent patients"); decision point is pre-arrival EMS transport selection, not an ED-based intake/triage/disposition action, despite the outcome event occurring in the ED. Matches the boundary doc's explicit pre-hospital/EMS exclusion category. SHAP is substantively used (not moot on F2) but Gate 1 failure is dispositive.
- `rayyan-601300489` — Exclude, E1. ED-to-ICU transfer-probability prediction (XGBoost+SHAP) fed into a Digital Twin explicitly consumed by "hospital administrators" for bed-allocation/capacity/staffing planning; paper's own Discussion names "interaction with clinicians" as a "pending gap," i.e., no clinician-in-loop. Administrative-consumption Gate 1/2/3 failure pattern (v2.2), same structural match as the boundary doc's own worked administrator-bed-allocation edge case.
- `rayyan-601300504` — Exclude, E3. AutoScore-based "SERP" interpretable point-score, multicenter external validation via common data model; all reported evaluation is of the underlying model's discrimination (AUROC, sensitivity, specificity, PPV/NPV) via CDM infrastructure, not of the score's interpretability itself. AutoScore is prior published work (not a novel method introduced here), so the MethodPaper exception's condition (a) is met only weakly and condition (b) (deliberate interpretability evaluation) is not met at all — classic SHAP/interpretable-score-as-decoration pattern.
- `rayyan-601300516` — Exclude, E4. Explicit "Protocol for System Development and Validation" (JMIR Research Protocols); Results section states modelling has not yet been performed ("study is currently being conducted... results expected to be published in 2022"). AutoScore-based interpretable design is the stated contribution but nothing has been evaluated yet. Clean Rule 7 protocol-only case, same pattern as `218`.
- `rayyan-601300564` — Exclude, E1. EMINENCE study predicts diagnostic yield of EEG acquisition (abnormal/epileptiform EEG, diagnosis confirmed/refuted) from admission clinical/anamnestic/neuroimaging data; despite the authors' repeated colloquial use of "triage" language, no ESI/CTAS/MTS/ATS-type acuity scale is computed and disposition is only a descriptive covariate, never a prediction target. Diagnostic-test-yield-prediction Gate 1 failure, same logic as the boundary doc's imaging-acquisition-for-diagnosis exclusion, applied here to EEG rather than imaging.

**Rationale:** This batch is dominated by two recurring failure patterns already established in prior batches: diagnostic/prognostic-differentiation Gate 1 failures (418, 454, 564, joining 077/067/293/326 — now 7 confirmed instances of this pattern) and format-driven E4 exclusions (431, 516, joining 218/269). `489` is a second confirmed instance of the administrative-consumption Gate 1/2/3 pattern. `504` reinforces the AutoScore/SERP-family E3 "evaluated the model, not the explanation" pattern already seen in `252`. No Include calls this batch — a run of 8/8 Exclude, the first fully-Exclude batch since the pilot.

**Impact:** `data/screening/fulltext_master_2026-07-06.csv` updated for `418`, `431`, `432`, `454`, `489`, `504`, `516`, `564` (`fulltext_screened="yes"`, all `Exclude`). Running full-text tally (re-verified directly against the master CSV, not narrative-summed): **36/64 screened, 5 Include, 31 Exclude, 28 remaining** in queue (5 of the 28 still blocked on retrieval: 220, 239, 248, 262, 267).

**Next:** Continue full-text screening of records with PDFs already in hand; chase retrieval for the 5-record pending set in parallel, not as a blocker.

---

## 2026-07-14 — Full-text screening: next batch of remaining 54 (626, 641, 644, 656, 257, 299, 312, 331; 626/312 blocked on PDF retrieval)

**Decision/Event:** User requested 626, 641, 644, 656, 257, 299, 312, 331. Confirmed via `fulltext_master_2026-07-06.csv` that `rayyan-601300626` and `rayyan-601300312` have `pdf_retrieved="no"` with no file present — deferred, not yet screenable. The remaining 6 were screened via `fulltext-screener` subagent against `docs/protocol/inclusion_boundary.md` v2.2 and `docs/protocol/screening_fulltext_criteria.md` v1.1. All 6 excluded (0 Include this batch — second consecutive fully-Exclude batch).

- `rayyan-601300641` — Exclude, E2. Pure LLM-vs-clinician accuracy/agreement comparison (ChatGPT 4o, Grok 3 vs. nurses/physicians assigning ESI triage levels); Gate 1 passes cleanly (ESI acuity scoring at ED arrival), but no explanation output from either LLM is ever elicited or evaluated — "black box" language appears only as a stated limitation and future-work item, never an applied method. Clean Gate-2/F2 failure, not a borderline E3/MethodPaper case.
- `rayyan-601300644` — Exclude, E1. NLP case-finding/referral-flagging model to intercept rheumatoid/psoriatic arthritis from ED clinical notes for rheumatology referral; retrospective 12-month look-back, no intake/triage/disposition action tied to the model's output ("triage" appears only as a covariate for control matching). Diagnostic-differentiation Gate 1 failure, text-data analogue of the imaging/lab-based pattern (077/067/293/326/418/454/564).
- `rayyan-601300656` — Exclude, E3. KTAS acuity-prediction model, strong Gate 1 fit; dedicated XAI section applies Permutation Importance, PDPs, and UMAP (satisfies F2), but all validation is narrative face-validity checking against the authors' own clinical intuition — no fidelity/stability metric, no clinician rating, no deployment study (paper's own Limitations concede real-time clinician interaction was not evaluated). Same "decoration" pattern as prior SHAP-as-decoration instances (252/504), applied here to permutation importance/PDP instead of SHAP.
- `rayyan-601300257` — Exclude, E3. FAIM fairness-mitigation framework applied to ED hospital-admission prediction (Gate 1 passes: admission is a disposition target); SHAP applied (satisfies F2) but used only descriptively to characterize how the fairness intervention shifted variable importance — all quantitative evaluation targets fairness metrics (equalized odds, BER equality) and model performance, never the SHAP explanation itself. MethodPaper exception rejected: stated primary contribution is fairness improvement, not an interpretability method.
- `rayyan-601300299` — Exclude, E1. Deterioration-prediction/track-and-trigger model (NEWS2-benchmarked) for the post-admission Emergency Admissions Unit (AMU-type ward), not the ED intake/triage/disposition point itself, despite ED-origin cohort and "emergency care decision making" title framing. Near-exact structural match to the boundary doc's own codified edge case ("sepsis deterioration model, ED-admitted cohort, inpatient-ward decision point → Exclude, population origin doesn't matter"). SHAP is applied (would satisfy F2) but only for plausibility-checking, not formally evaluated (would independently fail F3 if Gate 1 were judged to pass).
- `rayyan-601300331` — Exclude, E1. RAPIDx AI diagnostic-support tool for cardiac chest pain (diagnosing Type 1/Type 2 MI vs. myocardial injury from clinical + troponin data) — diagnostic-differentiation Gate 1 failure, not an intake/triage/disposition decision. PROLIFERATE_AI clinician evaluation (24 ED clinicians, usability/trust/adoption) is genuine clinician-in-the-loop work but evaluates the diagnostic tool overall, not an explanation/interpretability component; no named XAI method identified in the retrieved text (would also independently fail F2/E2).

**Rationale:** This batch introduces two new pattern variants while reinforcing existing ones: the diagnostic-differentiation Gate 1 pattern now extends to text/NLP data (`644`, first non-tabular/non-imaging instance) and to a second cardiac-diagnostic case (`331`, joining `418`); the deterioration/track-and-trigger inpatient-ward pattern (`299`) is the first live application of the boundary doc's own worked hypothetical edge case. The SHAP/interpretable-method "decoration" E3 pattern (evaluated the model or a fairness intervention, not the explanation) extends to a second technique family (`656`'s permutation importance/PDP/UMAP) and a second use case (`257`'s fairness-mitigation framing) beyond the AutoScore/SERP-specific instances (252/504). `641` is a new failure mode for this project: a general-purpose LLM applied directly to a Gate-1 task with zero explanation component, distinct from prior E2 calls which typically involved black-box models with no *stated* interpretability angle at all — here interpretability was explicitly discussed but only as an acknowledged limitation, not attempted.

**Impact:** `data/screening/fulltext_master_2026-07-06.csv` updated for `641`, `644`, `656`, `257`, `299`, `331` (`fulltext_screened="yes"`, all `Exclude`). `626`, `312` remain `fulltext_screened="no"` pending retrieval. Running full-text tally (re-verified directly against the master CSV, not narrative-summed): **42/64 screened, 5 Include, 37 Exclude, 22 remaining** in queue. A consolidated direct check of all `pdf_retrieved="no"` rows found **9 of the 22 remaining are retrieval-blocked**: 220, 239, 248, 262, 267, 312, 507, 537, 626 — all part of the original 9-record pending-retrieval set identified back on 2026-07-10 (see `project_fulltext_screening_progress.md` Retrieval status section); 507 and 537 simply hadn't come up in a requested batch until now, so this is the first time all 9 have been confirmed together in one direct query.

**Next:** Continue full-text screening of the 13 records with PDFs already in hand; chase retrieval for the 9-record pending set (220, 239, 248, 262, 267, 312, 507, 537, 626) in parallel, not as a blocker.

---

## 2026-07-14 — Full-text screening: next batch of remaining 54 (363, 375, 384, 407, 408)

**Decision/Event:** User requested 363, 375, 384, 407, 408. All 5 had `pdf_retrieved="yes"` with files on disk — no retrieval gaps this batch. All 5 screened via `fulltext-screener` subagent against `docs/protocol/inclusion_boundary.md` v2.2 and `docs/protocol/screening_fulltext_criteria.md` v1.1. First batch with an Include since Batch 5 (two straight fully-Exclude batches in between).

- `rayyan-601300363` — Exclude, E3. TBI elderly-patient ICU-vs-general-ward disposition model; Gate 1 passes cleanly (explicit "ICU triage disposition within 48h of ED admission" target), SHAP genuinely applied (F2 passes), but only narrated as clinically plausible feature rankings with a single illustrative force plot — no fidelity/stability metric, no clinician evaluation. Textbook SHAP-as-decoration E3, distinguished from E1 since Gate 1/2 substantively pass and only the evaluation component fails.
- `rayyan-601300375` — Exclude, E1. Sepsis-onset prediction from EHR events/vitals/labs (Sepsis-2 ground truth), the sole "triage" occurrence in the whole text is inside a cited reference's title, not the paper's own task description. Diagnostic/prognostic-differentiation Gate 1 failure, 3rd instance of the sepsis-prediction sub-pattern after `293`/`326`.
- `rayyan-601300384` — Exclude, E2. EBM/InterpretML (inherently interpretable GAM) model predicting MH-inpatient admission at ED triage; Gate 1 passes cleanly (admit/no-admit disposition target), interpretability explicitly framed as a study objective, but per Rule 1's conjunctive test no deliberate evaluation of the interpretability component was conducted — clinician engagement with the explanations is explicitly deferred to future work (Recommendations R1, R4). Coded E2 (not E3) per Rule 1's treatment of inherently-interpretable-model cases, same logic as `252`'s SERP+ call.
- `rayyan-601300407` — **Include.** Hymenopteran-sting severity/adverse-outcome risk-stratification model (death/CRRT/MODS) from initial vitals/labs at consultation, explicitly to guide ED physician treatment strategy; distinguished from diagnostic-differentiation because the underlying condition (confirmed sting) is already known, only severity/outcome is predicted — parallels the protocol's approved pediatric febrile-infant risk-stratification precedent. SHAP applied with a genuine stability proxy-metric evaluation (bootstrap coefficient-of-variation <15% across 100 resamples on the SHAP values themselves), satisfying F3 via Rule 3.
- `rayyan-601300408` — Exclude, E1. "Left against medical advice" (LAMA) prediction at triage; disposition-adjacent on its face, but the paper's own dedicated "Managerial impact" section (§4.7) routes the output to hospital administrators/managers for operational efficiency, throughput, and revenue purposes — zero mentions of "clinician" anywhere in the text, no clinical workflow described. Matches the v2.2 administrative-consumption edge case precedent (2nd exact structural match after `489`, 3rd counting the `252`-family conceptually). Would also independently fail F3 (E3-pattern SHAP narration), but E1 controls per the numeric tie-break.

**Rationale:** This batch breaks a run of 11 consecutive Exclude calls (Batches 6-7) with one Include (`407`), while also producing two more precise applications of established rules: `384` sharpens the E2-vs-E3 distinction for inherently-interpretable models (Rule 1's conjunctive framing+evaluation test puts the failure at F2 itself, not F3, unlike post-hoc-method cases), and `408` is the clearest administrative-consumption match yet (an entire dedicated paper section named "Managerial impact" with zero clinician mentions). `375` extends the sepsis-prediction diagnostic-differentiation sub-pattern to a third instance. `407` is the second risk-stratification-of-a-known-condition Include (after the pediatric febrile-infant protocol precedent it was checked against), reinforcing that this is a stable, distinct Include-side pattern from the diagnostic-differentiation Exclude-side pattern.

**Impact:** `data/screening/fulltext_master_2026-07-06.csv` updated for `363`, `375`, `384`, `407`, `408` (`fulltext_screened="yes"`). Running full-text tally (re-verified directly against the master CSV, not narrative-summed): **47/64 screened, 6 Include, 41 Exclude, 17 remaining** in queue (9 of the 17 still blocked on PDF retrieval: 220, 239, 248, 262, 267, 312, 507, 537, 626).

**Next:** Continue full-text screening of the 8 records with PDFs already in hand; chase retrieval for the 9-record pending set in parallel, not as a blocker.

---

## 2026-07-14 — Full-text screening: next batch of remaining 54 (426, 441, 507, 537, 549; 507/537 blocked on PDF retrieval)

**Decision/Event:** User requested 426, 441, 507, 537, 549. Confirmed via `fulltext_master_2026-07-06.csv` that `rayyan-601300507` and `rayyan-601300537` have `pdf_retrieved="no"` with no file present — both part of the previously-identified 9-record pending-retrieval set. The remaining 3 were screened via `fulltext-screener` subagent against `docs/protocol/inclusion_boundary.md` v2.2 and `docs/protocol/screening_fulltext_criteria.md` v1.1. All 3 excluded (0 Include this batch).

- `rayyan-601300426` — Exclude, E1. Pediatric ED sepsis-onset prediction from labs/vitals, triggering a tiered treatment-escalation protocol (nurse vigilance → ICU team alert → physician-initiated sepsis-management bundle); zero grep hits for disposition/discharge/triage as decision outputs, "admit"/"transfer" appear only in cohort-definition/outcome language. Diagnostic-differentiation Gate 1 failure, 4th sepsis-prediction instance after `293`/`326`/`375`. Distinguished from the `249`/`505` ICU-transfer Include precedent because the model output here triggers monitoring/treatment actions, not an explicit admit/transfer decision.
- `rayyan-601300441` — Exclude, E2. Paediatric-ED "avoidable patient" fast-track redirection decision support system; Gate 1 passes cleanly (nurse-actioned redirection at triage). Models evaluated on a named "complexity, interpretability, and predictive performance" framework with a pruned decision tree selected as "glass box," but interpretability is asserted/selected-for, never deliberately evaluated (no proxy metric, no clinician study of tree comprehension/trust) — Rule 1's second prong fails. Coded E2 (not E3) since no post-hoc explanation *method* was ever applied to leave unevaluated; the tree-diagram presentation itself is the unevaluated interpretability claim, same logic as `384`'s EBM case.
- `rayyan-601300549` — Exclude, E3. KTAS acuity-classification from speech/NLP in a role-played (not synthetic-data) simulation study; Gate 1 passes cleanly (KTAS is a named in-scope acuity scale). SHAP applied to all four classifiers (F2 passes) with a results table of top attributed words, but evaluation is narrative face-validity discussion only — no fidelity/stability metric, no clinician rating, no deployment study. Identical KTAS/SHAP-decoration pattern to `076` and `656`, now a 3rd confirmed instance on this specific subtopic.

**Rationale:** This batch reinforces three established patterns rather than introducing new ones: sepsis-prediction diagnostic-differentiation reaches a 4th instance (`426`), the KTAS/SHAP-decoration sub-pattern reaches a 3rd instance (`549`, following `076` and `656`), and `441` provides a second clean application of the E2-for-inherently-interpretable-models distinction first sharpened by `384` in the prior batch (asserted-but-unevaluated interpretability claims fail at F2 itself, not F3).

**Impact:** `data/screening/fulltext_master_2026-07-06.csv` updated for `426`, `441`, `549` (`fulltext_screened="yes"`, all `Exclude`). `507`, `537` remain `fulltext_screened="no"` pending retrieval. Running full-text tally (re-verified directly against the master CSV, not narrative-summed): **50/64 screened, 6 Include, 44 Exclude, 14 remaining** in queue (9 of those 14 still blocked on PDF retrieval: 220, 239, 248, 262, 267, 312, 507, 537, 626).

**Next:** Continue full-text screening of the 5 records with PDFs already in hand; chase retrieval for the 9-record pending set in parallel, not as a blocker.

---

## 2026-07-14 — Full-text screening: next batch of remaining 54 (560, 584, 595, 657, 673) — all PDF-retrievable records now screened

**Decision/Event:** User requested 560, 584, 595, 657, 673. All 5 had `pdf_retrieved="yes"` with files on disk — no retrieval gaps this batch. All 5 screened via `fulltext-screener` subagent against `docs/protocol/inclusion_boundary.md` v2.2 and `docs/protocol/screening_fulltext_criteria.md` v1.1. 1 Include, 4 Exclude. This batch clears every record in `fulltext_remaining_54_2026-07-10.csv` that has a PDF in hand — all 9 records still unscreened are blocked on retrieval.

- `rayyan-601300560` — Exclude, E1. ED-evaluated suspected-PE in-hospital-mortality prediction; grep found only background/future-work framing around "disposition" and "triage" (e.g., "prospective implementation studies are needed... before deployment as decision support"), no present-tense Methods sentence tying the model's output to a current ED action. 5th prognostic/mortality-prediction Gate-1 failure alongside the sepsis cluster (293/326/375/426), distinguished from the `407` Include precedent by the absence of any "guide ED physician treatment strategy"-type present-tense task framing.
- `rayyan-601300584` — Exclude, E1. "Accuracy is not enough" EBM sepsis-risk model; despite strong interpretability framing (EBM, explicit title/abstract emphasis) and elaborated future-integration language ("real-time integration... could optimize triage workflows"), all triage/disposition language is confined to the Discussion as speculative future work — no Methods-level decision-point tie. 6th sepsis-prediction diagnostic-differentiation instance after 293/326/375/426/... (this batch's own `560` is a different condition, not counted in the sepsis-specific count). Would also independently support E3 (EBM interpretability framed but never evaluated), but E1 controls per Gate 1 substantively failing first.
- `rayyan-601300595` — **Include.** Falls-in-older-adults "serious disposition" (admission/transfer/death) risk-stratification model at ED triage, using ED clinical narratives (NLP) + survival modelling; disposition outcome explicitly defined and tied to the ED triage action point in Methods. LIME applied with a genuine quantitative stability procedure (signal-to-noise ratio ≥0.8, sign-consistency ≥0.6 across narratives, bootstrap CIs) — a real computed stability metric on the explanation output, satisfying F3 via Rule 3, distinguished from `673`'s narrative-only "consistency" claim in the same batch.
- `rayyan-601300657` — Exclude, E2. SERP integrated with ED triage (PACS+) to predict 30-day mortality — the flagged sibling of `391`/`252`. Gate 1 passes cleanly (explicit PACS triage-category reassignment at ED arrival). Applying the same Rule 1 two-prong test used for the 391/252 contrast: interpretability is framed more strongly than `252` ("pioneers the integration of interpretable ML... to support clinician trust and usability"), but the paper's own Limitations section explicitly admits interpretability was never evaluated ("Our study did not evaluate these workflow or safety implications"). Lands on the same E2 outcome as `252` since the evaluation prong is what's decisive, not framing strength.
- `rayyan-601300673` — Exclude, E3. EMS-transported-patient ED-triage outcome model comparing manual triage systems (ESI/MTS/TMHTS) vs. ML; Gate 1 confirmed as ED-arrival triage, not pre-hospital (physicians explicitly "not influenced by ML model outputs," ruling out the pre-hospital/EMS exclusion category despite the EMS-transport population). SHAP applied to both tree models but only narratively described as "consistent... supporting stability," with no reported statistic — distinguished from `595`'s genuine computed metric in the same batch.

**Rationale:** This batch resolves the flagged `391`/`252`/`657` SERP-family follow-up (E2, consistent outcome despite stronger framing — confirming framing strength alone doesn't flip the call, only the evaluation prong does) and produces a clean same-batch contrast pair on the Rule-3 proxy-metric threshold: `595` (Include, genuine computed SNR/sign-consistency stability statistic) vs. `673` (Exclude E3, narrative-only "consistent" claim with no reported statistic) — reinforcing the `407`-established distinction between a real quantitative stability check and mere plausibility narration. `560`/`584` extend the prognostic/diagnostic-differentiation Gate-1 exclusion cluster, both notable for unusually elaborated future-integration language that nonetheless remains speculative rather than descriptive of a current action.

**Impact:** `data/screening/fulltext_master_2026-07-06.csv` updated for `560`, `584`, `595`, `657`, `673` (`fulltext_screened="yes"`). Running full-text tally (re-verified directly against the master CSV, not narrative-summed): **55/64 screened, 7 Include, 48 Exclude, 9 remaining** in queue — all 9 remaining records are the retrieval-blocked set (220, 239, 248, 262, 267, 312, 507, 537, 626); every PDF-in-hand record has now been screened.

**Next:** Chase PDF retrieval for the final 9-record pending set; no further records can be screened until at least one of these is retrieved.

---

## 2026-07-14 — Differential-window search update (2026-06-11 to 2026-07-14): 0 new Includes from 46 net-new candidates

**Decision/Event:** With the main screening queue exhausted (all screenable records done, 9 remaining blocked on retrieval), the user asked how to add more Includes to the corpus. Rather than re-running the already-covered Jan-Dec 2024 window (would have been pure duplication — the EM-narrowed v2 FINAL PubMed string was already executed 2026-06-10 with date range 2015/01/01-2026/06/10, per the 2026-06-10 decision log entry), a genuinely new differential window was identified and searched: **2026-06-11 through 2026-07-14** (the gap since last execution), using the exact same registered A+B+C v2 FINAL string (`docs/protocol/search_string_pubmed_v1.md`).

**Search execution:** 53 raw hits via E-utilities esearch. 7 were already present in the existing 650-record corpus (PMIDs with `Date - Publication` metadata that shifted to fall after 2026-06-10 post-indexing — a known Epub-ahead-of-print reclassification issue already documented in the 2026-06-09 date-range decision entry) — all 7 confirmed already correctly adjudicated (6 Exclude, 1 Exclude-on-borderline-adjudication). **46 net-new candidates** remained. Raw export: `data/searches/pubmed_diff_2026-06-11_to_2026-07-14.txt` (all 53); net-new abstracts: `data/searches/pubmed_diff_netnew_46_2026-07-14.txt`.

**T/A screening (46 records, via `ta-screener` subagent in 6 parallel batches):** 5 Include, 2 Maybe/Borderline, 39 Exclude. Dominant Exclude pattern: bare "triage" keyword matches in clearly non-ED domains (oncology, dermatology, pathology, vestibular medicine, TB, hematology) — the search string's known sensitivity-favoring false-positive pattern, consistent with prior batches. A handful of ICU/inpatient/primary-care decision-point failures and review/protocol format failures rounded out the Excludes.

**Full-text screening (7 candidates forwarded — 5 Include + 2 Maybe, since both Maybe cases hinged on questions full-text resolves directly):**
- PMID 42303803 (Henn et al., emergency-surgery-need prediction, abdominal pain) — Exclude E1. "Urgent surgery within 24h" is a treatment/diagnostic-need classification, not an admit/discharge/transfer disposition action; matches the established CPR/shockable-rhythm in-ED-treatment-decision exclusion precedent. Flagged as a genuinely close call by the screener.
- PMID 42327624 (Ahmed et al., LLM-SHAP mental-health ED-return prediction) — Exclude E1. Despite a genuinely well-evaluated LLM-SHAP explanation framework (F2/F3 would both pass), the paper never describes a current ED workflow step where a clinician acts on the score; authors themselves state clinical decision-making impact "was not formally evaluated."
- PMID 42410788 (ISAR+CIRS dual-scale model, older-adult 30-day outcomes) — Exclude E1. Triage level is used only as an input feature, not reassigned as an output; "disposition planning" language is hedged ("may consider") and confined to Discussion/Results commentary, not a Methods-level decision-point definition. Also independently fails F3 (SHAP narrated only; paper explicitly disclaims causal/independent-validation interpretation).
- PMID 42418473 (pediatric bronchopneumonia vs. URTI differentiation) — Exclude E1. Diagnostic-differentiation from routine labs, mixed outpatient/ED cohort — same pattern as `rayyan-601300632`, excluded earlier in this same differential batch at T/A.
- PMID 42421084 (Chen et al., cardio-respiratory DL, ED-triage admission prediction) — Exclude E3. Gates 1-2 pass cleanly (genuine ED-triage admission/disposition decision, Score-CAM applied), but Score-CAM is shown only as two illustrative case-figure overlays with an explicit authorial disclaimer that the visualization is "hypothesis-generating," not evaluated. Retrieval note: the initially-scraped landing-page HTML was insufficient (abstract only); the screening subagent independently retrieved the full 31-page manuscript PDF directly from the publisher, now saved as `data/extraction/fulltext_pdfs/rayyan-diff-42421084.pdf`.
- PMID 42277719 (bronchiolitis prediction, children under 2) — Exclude E1. Case-control diagnostic-differentiation task (bronchiolitis vs. not), dispositive regardless of the setting ambiguity flagged at T/A ("5 pediatric centers" never confirmed as EDs in the retrievable text — only the abstract/landing page was retrievable for this record, `rayyan-diff-42277719.html`).
- PMID 42393983 (FT-Transformer DeepSurv, post-discharge mortality) — **not screened**, PDF retrieval blocked. This is an IOS Press *Studies in Health Technology and Informatics* book-chapter (confirmed via Unpaywall metadata: `genre: book-chapter`), consistent with the T/A-stage concern that this may be a short conference-proceedings entry rather than a full paper. Added to the retrieval-blocked list.

**Rationale:** This batch is a useful negative result, not a wasted effort: it confirms the main corpus's established exclusion patterns (diagnostic-differentiation, in-ED-treatment-decision, SHAP/XAI-as-decoration, aspirational-future-work-only Gate-1 language) generalize cleanly to freshly-published literature outside the original search window, rather than being artifacts of the specific 2015-2026/06/10 corpus. Notably, 4 of the 5 T/A-stage Includes failed at full-text specifically on the "no described current ED action point" sub-pattern (aspirational/future-work framing substituting for an actual workflow description) — this is now a well-established recurring full-text-stage correction of T/A-stage optimism, not a one-off.

**Impact:** No change to `data/screening/fulltext_master_2026-07-06.csv` (these are differential-search records outside that file's scope, tracked separately per this entry and `data/searches/pubmed_diff_*` files). **Total Include count remains 7** (unchanged from the main corpus). One additional record (42393983) added to the retrieval-blocked list, now 10 total blocked records across both the main corpus and this differential batch.

**Next:** If further corpus expansion is desired, higher-yield options remain: (1) verify whether the Embase/IEEE Xplore/ACM Digital Library EM-narrowed translations were formally executed beyond PubMed (IEEE and ACM were executed 2026-06-18/22 per `prisma_counts.csv`; Embase was dropped for lack of institutional access) — IEEE/ACM's own differential windows (post-06-18/06-22) remain unswept; (2) execute the supplementary search plan (`docs/protocol/supplementary_search_plan.md`) — forward citation-chasing from the 7 Included papers, Elicit semantic search; (3) chase legitimate alternative retrieval (Unpaywall/OA button, author email, ILL) for the now-10-record retrieval-blocked set, at an observed ~13% historical inclusion rate.

---

## 2026-07-14 — Screening closed at 7 included studies; corpus-growth avenues deliberately not pursued further

**Decision:** The review's included-study corpus is finalized at **7 studies** (rayyan-601300063, 068, 083, 366, 391, 407, 595). No further corpus-growth activity (additional differential search windows, IEEE/ACM re-sweeps, citation-chasing, or continued chasing of the 10 retrieval-blocked records) will be pursued. Full-text screening of the main 64-record queue and the 2026-07-14 differential-search supplement are both closed out as complete for the purposes of this review.

**Rationale:** After the main queue was exhausted (55/64 screened, 9 blocked on retrieval with no viable access path at this institution) and a differential search of the 2026-06-11–2026-07-14 gap window yielded 46 new candidates but zero additional Includes (see entry immediately above), the user made an explicit time-allocation decision to proceed with the corpus as-is rather than continue investing reviewer time chasing marginal yield. This is consistent with the project's standing 8-week single-reviewer timeline constraint (2026-06-10 pivot decision) and the JBI/PRISMA-ScR scoping-review methodology already adopted, which does not require a minimum study count — the review question is answerable via narrative synthesis organized around RQ1-RQ3 regardless of corpus size, and a small, deeply-characterized corpus is arguably a better fit for the grading rubric's "argue, not summarize" emphasis than a larger, shallower one would be.

**Alternatives considered:**
- Continue pursuing the 3 higher-yield options identified in the prior entry (IEEE/ACM differential re-sweep, citation-chasing, alternative retrieval for the 10 blocked records) — rejected as a time/yield trade-off: the just-completed differential search demonstrated that even a well-targeted new search window can return 46 candidates and 0 net Includes, and the historical inclusion rate (~13% of screened records, and far lower per unit of reviewer time spent on search/retrieval infrastructure) does not justify further investment given the course timeline.
- Treat 7 as provisional and revisit if time permits later in Phase 3 — not rejected outright, but not the active plan; if time becomes available, the three higher-yield options remain documented and ready to execute.

**Impact:** `data/screening/prisma_counts.csv` "Included: Studies included in review" row finalized at **7**, with the full E1-E6 breakdown recorded (E1=22, E2=5, E3=13, E4=8, E5=0, E6=0, total excluded=48, total assessed=55, 9 not assessed/retrieval-blocked). Extraction (Milestone 4) can now proceed against this fixed 7-study corpus. The 10 retrieval-blocked records (main corpus: 220, 239, 248, 262, 267, 312, 507, 537, 626; differential batch: 42393983) remain logged as a documented, disclosed limitation (institutional-access gap) rather than silently dropped, per this project's standing transparency convention — to be reported in the manuscript's limitations section and PRISMA-ScR flow diagram as "not retrievable," distinct from full-text-assessed-and-excluded records.

**Defense if challenged:** "The corpus was not capped arbitrarily at 7 — it reflects the full outcome of (a) exhaustive screening of the registered 64-record T/A-forwarded queue down to the 9 records genuinely unretrievable at this institution, and (b) a targeted differential search update covering the full gap since last search execution, using the same registered, recall-validated search string. That differential search is itself evidence the corpus is not under-sampled: it returned 46 new candidates and confirmed the review's established exclusion patterns generalize to freshly-published literature rather than being artifacts of the original search window. Further growth was assessed as low-yield relative to reviewer time remaining in an 8-week single-reviewer timeline, a documented and registered constraint from the project's 2026-06-10 scope pivot. JBI scoping review methodology does not impose a minimum study count; the review's narrative synthesis is structured around RQ1-RQ3 regardless of corpus size. All retrieval gaps are disclosed, not concealed, in the PRISMA-ScR flow diagram."

---
