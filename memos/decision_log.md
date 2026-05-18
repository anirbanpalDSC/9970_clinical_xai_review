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
