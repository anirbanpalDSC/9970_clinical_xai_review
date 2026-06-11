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
