# PRISMA-ScR Checklist

**Reporting standard:** PRISMA Extension for Scoping Reviews (PRISMA-ScR) — Tricco AC, Lillie E, Zarin W, et al. PRISMA Extension for Scoping Reviews (PRISMA-ScR): Checklist and Explanation. *Ann Intern Med.* 2018;169(7):467-473.

**IMPORTANT — verify before submission:** Item wording and numbering below were reconstructed from memory of the published checklist, not copied from the primary source. Cross-check every item's exact wording and section grouping against the original Tricco et al. 2018 checklist (freely available at equator-network.org and as the article's supplement) before finalizing — reviewers and editors check submissions against the official checklist PDF directly, and any drift in item wording is an easy, avoidable desk-reject flag.

**How to use this file:** Each row states (a) whether/where the item is addressed in this project's current state, and (b) a `Page #` placeholder to fill in once the manuscript is typeset. Items marked **PENDING** depend on work not yet done (extraction, synthesis, manuscript drafting) as of this file's creation (2026-07-18) — revisit and complete those rows as that work finishes.

---

## Title

| # | Item | Reported? | Location / Notes | Page # |
|---|------|-----------|-------------------|--------|
| 1 | Identify the report as a scoping review. | Yes | Title includes "A Scoping Review": *"Beyond Fidelity: Evaluating the Validity of Explainable AI in Emergency Department Triage and Disposition — A Scoping Review."* | ___ |

## Abstract

| # | Item | Reported? | Location / Notes | Page # |
|---|------|-----------|-------------------|--------|
| 2 | Structured summary (background, objectives, eligibility criteria, sources of evidence, charting methods, results, conclusions). | **PENDING** | Abstract not yet drafted. Draft as a structured abstract once Results/Discussion are written, since it should summarize final numbers (7 included studies) and RQ1-RQ3 findings, not projected ones. | ___ |

## Introduction

| # | Item | Reported? | Location / Notes | Page # |
|---|------|-----------|-------------------|--------|
| 3 | Rationale — describe the rationale in the context of what is already known; explain why the questions/objectives lend themselves to a scoping (not systematic) review approach. | **PENDING** (content exists, not yet drafted into manuscript prose) | Rationale is established in `docs/osf/preregistration_draft.md` §1 (Background and Rationale) and the "Beyond Fidelity" framing — XAI evaluation maturity in EM, regulatory timeliness (EU AI Act Article 13, FDA AI/ML guidance). Needs to be written into the Introduction. | ___ |
| 4 | Objectives — explicit statement of questions/objectives with key elements (population, concepts, context). | **PENDING** (content exists) | RQ1-RQ3 fully specified in `docs/osf/preregistration_draft.md` §7 (Synthesis). State verbatim at the end of the Introduction. | ___ |

## Methods

| # | Item | Reported? | Location / Notes | Page # |
|---|------|-----------|-------------------|--------|
| 5 | Protocol and registration — state whether a protocol exists, where accessible, and registration number if available. | Yes (content ready) | OSF registration: `docs/osf/preregistration_draft.md`, filed 2026-05-24, revised to Draft v2.2 (2026-06-22) following the 2026-06-10 EM-scope pivot. PROSPERO explicitly **not** used — deprioritized 2026-06-10 (`docs/osf/prospero_draft.md` status note; `memos/decision_log.md`), state as a disclosed methodological choice, not an omission, and reframe the rationale for an academic audience rather than citing the grading rubric directly. | ___ |
| 6 | Eligibility criteria — characteristics used as inclusion/exclusion criteria (e.g., years, language, publication status), with rationale. | Yes (content ready) | 3-gate boundary in `docs/protocol/inclusion_boundary.md` v2.2: (a) decision point occurs during the initial ED encounter — intake, acuity/ESI scoring, or immediate disposition; (b) an explainable/interpretable AI method is applied; (c) an empirical evaluation component is reported. Date range 2015-01-01 through search-execution date (rolling; extended by the 2026-07-14 differential update through 2026-07-14). English language only. Rationale for the EM-only scope: 2026-06-10 pivot decision (8-week single-reviewer timeline; see decision log). | ___ |
| 7 | Information sources — all sources searched, including dates of coverage and most recent search date. | Yes (content ready) | PubMed (searched 2015-01-01 through 2026-06-10, formally executed; differential update 2026-06-11 through 2026-07-14), IEEE Xplore (executed 2026-06-18), ACM Digital Library (executed 2026-06-22, via OpenAlex API substitution — disclose the methodology deviation and why). **Embase considered but dropped** (2026-06-22, no institutional access — disclose as limitation). CINAHL considered, shelved per the EM-narrowed scope decision (not part of primary search). Most recent search date: **2026-07-14**. | ___ |
| 8 | Search — full electronic search strategy for at least one database, repeatable. | Yes (content ready) | Full PubMed A+B+C v2 FINAL string in `docs/protocol/search_string_pubmed_v1.md` (497 records, 2015-01-01 to 2026-06-10) plus the differential-window string (2026-06-11 to 2026-07-14, identical term structure). IEEE and ACM strings in their respective `docs/protocol/search_string_*.md` files. Present at least the PubMed string in full in a supplementary table/box; the others can go in supplementary material. | ___ |
| 9 | Selection of sources of evidence — process for selecting sources (screening and eligibility). | Yes (content ready) | Title/abstract screening: Rayyan, single reviewer, sensitivity-favoring 3-gate criteria (`docs/protocol/screening_criteria.md`), TA-E1–E5 exclusion taxonomy. Full-text screening: F1-F5 criteria + E1-E6 exclusion taxonomy (`docs/protocol/screening_fulltext_criteria.md` v1.1). **Sole-reviewer status** at both T/A and full-text stages, faculty-confirmed accommodation given supervisor availability constraints (`memos/decision_log.md`, "Faculty adjudication delegated" and 2026-07-10 entries) — state this plainly as a disclosed deviation from the two-independent-reviewer standard. | ___ |
| 10 | Data charting process — methods used to chart data (forms, independent/duplicate charting, process for confirming data with investigators). | **PENDING** (extraction not yet performed) | Charting tool: `data/extraction/schema_v1.csv` (v1.3, 39 columns), documented in `data/extraction/schema_README.md`. **Sole reviewer, no independent duplicate charting** — same faculty-confirmed accommodation as screening; formal inter-rater kappa not computed for the same disclosed reason (no viable washout period within the timeline). State this explicitly, do not imply duplicate charting occurred. | ___ |
| 11 | Data items — list and define all variables sought, with assumptions/simplifications. | Yes (content ready, pending extraction completion) | Full column definitions in `data/extraction/schema_README.md`: clinical domain, XAI method/scope (`docs/protocol/xai_method_taxonomy.md`), study design/participants, evaluation type (`data/coding/eval_type_taxonomy.md`), workflow realism (`data/coding/workflow_realism_rubric.md`), 4-dimension ecological validity, clinician involvement (evaluation vs. design, kept separate by design), outcomes claimed vs. demonstrated, trust-claim type (calibration vs. plausibility distinction), 5-dimension quality/risk-of-bias, method-justification type (RQ1), interpretability-framework classification (Doshi-Velez & Kim; Vilone & Longo), 4 regulatory-evidence criteria (RQ3), semantic tags. | ___ |
| 12 | Critical appraisal of individual sources of evidence — rationale, methods, and how used in synthesis (if done). | Yes (content ready) | Custom 5-dimension rubric (QR1-QR5: Participant Appropriateness, Task Fidelity, Outcome Measurement, Explanation Faithfulness, Reporting Completeness — `data/coding/quality_rubric.md`), adapted from QUADAS-2/RoB 2/TRIPOD elements plus two dimensions with no standard-tool equivalent (rationale: `memos/decision_log.md`, 2026-05-26 entry). Used as a supplementary/exploratory characterization of the corpus, **not** as an inclusion/exclusion filter — state this explicitly to avoid the appraisal reading as a second screening pass. | ___ |
| 13 | Synthesis of results — methods for handling/summarizing charted data. | Yes (content ready) | Narrative synthesis organized by RQ1-RQ3 (JBI methodology, Peters et al. 2020; PRISMA-ScR, Tricco et al. 2018) — not confirmatory hypothesis testing. The originally-planned H1-H6 hypotheses and quality-rubric scores are repositioned as supplementary/exploratory analyses feeding the RQ2 narrative, not primary confirmatory tests (2026-06-10 pivot decision). | ___ |

## Results

| # | Item | Reported? | Location / Notes | Page # |
|---|------|-----------|-------------------|--------|
| 14 | Selection of sources of evidence — numbers screened/assessed/included, reasons for exclusion at each stage, ideally a flow diagram. | Yes (numbers finalized, diagram not yet built) | All numbers finalized in `data/screening/prisma_counts.csv`: 659 identified (497 PubMed + 161 IEEE + 1 ACM) → 650 after deduplication → 650 screened at T/A → 64 forwarded to full-text → 55 assessed at full-text (**9 not retrievable**, disclosed separately from exclusions) → 48 excluded (E1=22, E2=5, E3=13, E4=8, E5=0, E6=0) → **7 included**. Separately: a 2026-07-14 post-hoc differential-search supplement screened 46 additional candidates, added 0 studies (does not change the 7). Build the PRISMA-ScR flow diagram from these numbers — happy to help construct it (TikZ/draw.io) once you're ready. | ___ |
| 15 | Characteristics of sources of evidence — present charted characteristics per source, with citations. | **PENDING** (extraction not yet performed) | Will be a per-paper summary table once extraction completes; citations in `references/bib/included_studies.bib` (7 entries, verified against CrossRef). | ___ |
| 16 | Critical appraisal within sources of evidence — present appraisal data (if done). | **PENDING** (extraction not yet performed) | QR1-QR5 scores per included paper, once extraction completes. | ___ |
| 17 | Results of individual sources of evidence — relevant charted data per included source. | **PENDING** (extraction not yet performed) | Per-paper extracted data (XAI method, eval type, realism level, trust claim, etc.), once extraction completes. | ___ |
| 18 | Synthesis of results — summarize/present charting results as they relate to the review questions. | **PENDING** (synthesis not yet performed) | RQ1 (methods deployed + justification), RQ2 (evaluation rigor across involvement levels), RQ3 (regulatory-readiness evidence) narrative subsections, once extraction/synthesis complete. | ___ |

## Discussion

| # | Item | Reported? | Location / Notes | Page # |
|---|------|-----------|-------------------|--------|
| 19 | Summary of evidence — main results (overview of concepts/themes/evidence types), link to questions/objectives, relevance to key groups. | **PENDING** (depends on synthesis) | Likely headline finding based on screening-stage exclusion patterns already observed: a substantial share of EM XAI literature applies an explanation method without ever evaluating it (13/48 full-text exclusions were E3 alone) — worth previewing this as a signal of what the Discussion's summary-of-evidence will likely emphasize. | ___ |
| 20 | Limitations — discuss limitations of the scoping review process. | Yes (content ready, not yet drafted into prose) | Concrete, already-disclosed items to write from: Embase dropped (no institutional access); CINAHL shelved; English-language-only restriction; single reviewer with no independent duplicate screening/charting and no formal IRR kappa at full-text and extraction stages (faculty-confirmed accommodation, explicitly disclosed rather than concealed); 10 records never retrieved and thus never assessed (9 main-corpus + 1 differential-supplement); small final corpus (n=7) — note this is methodologically appropriate for scoping review synthesis, not a defect, but still worth naming as a scope limitation; 2015 search start date. | ___ |
| 21 | Conclusions — general interpretation relative to questions/objectives, implications, next steps. | **PENDING** (depends on synthesis) | | ___ |

## Funding

| # | Item | Reported? | Location / Notes | Page # |
|---|------|-----------|-------------------|--------|
| 22 | Funding — sources of funding for included studies and for the review itself; role of funders. | Yes | **No funding was received for this review.** State this plainly in the manuscript's Funding/Declarations section (e.g., "This research received no specific grant from any funding agency in the public, commercial, or not-for-profit sectors."). | ___ |

---

## Completion Status Summary

- **Ready to write now** (all underlying facts already exist in project files): Items 1, 5, 6, 7, 8, 9, 11 (definitions), 12, 13, 14 (numbers only, not diagram), 20, 22 (funding — confirmed none).
- **Blocked on extraction** (Milestone 4, not yet started): Items 10 (process description can be written now; actual charting is pending), 11 (per-paper values), 15, 16, 17.
- **Blocked on synthesis/drafting**: Items 2, 3, 4, 18, 19, 21.
- **Needs your input, not derivable from project files**: none remaining.
