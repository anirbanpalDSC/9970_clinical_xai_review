# PRISMA-ScR Checklist

**Reporting standard:** PRISMA Extension for Scoping Reviews (PRISMA-ScR) — Tricco AC, Lillie E, Zarin W, et al. PRISMA Extension for Scoping Reviews (PRISMA-ScR): Checklist and Explanation. *Ann Intern Med.* 2018;169(7):467-473.

**IMPORTANT — verify before submission:** Item wording and numbering below were reconstructed from memory of the published checklist, not copied from the primary source. Cross-check every item's exact wording and section grouping against the original Tricco et al. 2018 checklist (freely available at equator-network.org and as the article's supplement) before finalizing — reviewers and editors check submissions against the official checklist PDF directly, and any drift in item wording is an easy, avoidable desk-reject flag.

**How to use this file:** Each row states (a) whether/where the item is addressed in this project's current state, and (b) a `Page #` placeholder to fill in once the manuscript is typeset. As of 2026-07-26, extraction, synthesis, and manuscript drafting (Abstract through Conclusion) are complete; all 22 items are reported. `Page #` columns remain placeholders pending final typesetting for a specific journal template.

---

## Title

| # | Item | Reported? | Location / Notes | Page # |
|---|------|-----------|-------------------|--------|
| 1 | Identify the report as a scoping review. | Yes | Title includes "A Scoping Review": *"Beyond Fidelity: Evaluating the Validity of Explainable AI in Emergency Department Triage and Disposition — A Scoping Review."* | ___ |

## Abstract

| # | Item | Reported? | Location / Notes | Page # |
|---|------|-----------|-------------------|--------|
| 2 | Structured summary (background, objectives, eligibility criteria, sources of evidence, charting methods, results, conclusions). | Yes | Abstract (`manuscript_v1.md`), structured as Background/Objective/Methods/Results/Conclusions, reporting final numbers (7 included studies) and RQ1-RQ3 findings. | ___ |

## Introduction

| # | Item | Reported? | Location / Notes | Page # |
|---|------|-----------|-------------------|--------|
| 3 | Rationale — describe the rationale in the context of what is already known; explain why the questions/objectives lend themselves to a scoping (not systematic) review approach. | Yes | Introduction (`manuscript_v1.md`), opening paragraphs plus "Where this review sits relative to existing literature," establishing the interpretability/trust-calibration/evaluation-validity framing, the regulatory-timeliness rationale, and the literature gap this scoping (not systematic) review addresses. | ___ |
| 4 | Objectives — explicit statement of questions/objectives with key elements (population, concepts, context). | Yes | Introduction, "Research questions" (`manuscript_v1.md`): RQ1-RQ3 stated verbatim, with population (EM decision points), concepts (interpretability, trust calibration, evaluation validity), and context (regulatory-evidence expectations) specified. | ___ |

## Methods

| # | Item | Reported? | Location / Notes | Page # |
|---|------|-----------|-------------------|--------|
| 5 | Protocol and registration — state whether a protocol exists, where accessible, and registration number if available. | Yes (content ready) | OSF registration: `docs/osf/preregistration_draft.md`, filed 2026-05-24, revised to Draft v2.2 (2026-06-22) following the 2026-06-10 EM-scope pivot. PROSPERO explicitly **not** used — deprioritized 2026-06-10 (`docs/osf/prospero_draft.md` status note; `memos/decision_log.md`), state as a disclosed methodological choice, not an omission, and reframe the rationale for an academic audience rather than citing the grading rubric directly. | ___ |
| 6 | Eligibility criteria — characteristics used as inclusion/exclusion criteria (e.g., years, language, publication status), with rationale. | Yes (content ready) | 3-gate boundary in `docs/protocol/inclusion_boundary.md` v2.2: (a) decision point occurs during the initial ED encounter — intake, acuity/ESI scoring, or immediate disposition; (b) an explainable/interpretable AI method is applied; (c) an empirical evaluation component is reported. Date range 2015-01-01 through search-execution date (rolling; extended by the 2026-07-14 differential update through 2026-07-14). English language only. Rationale for the EM-only scope: 2026-06-10 pivot decision (8-week single-reviewer timeline; see decision log). | ___ |
| 7 | Information sources — all sources searched, including dates of coverage and most recent search date. | Yes (content ready) | PubMed (searched 2015-01-01 through 2026-06-10, formally executed; differential update 2026-06-11 through 2026-07-14), IEEE Xplore (executed 2026-06-18), ACM Digital Library (executed 2026-06-22, via OpenAlex API substitution — disclose the methodology deviation and why). **Embase considered but dropped** (2026-06-22, no institutional access — disclose as limitation). CINAHL considered, shelved per the EM-narrowed scope decision (not part of primary search). Most recent search date: **2026-07-14**. | ___ |
| 8 | Search — full electronic search strategy for at least one database, repeatable. | Yes (content ready) | Full PubMed A+B+C v2 FINAL string in `docs/protocol/search_string_pubmed_v1.md` (497 records, 2015-01-01 to 2026-06-10) plus the differential-window string (2026-06-11 to 2026-07-14, identical term structure). IEEE and ACM strings in their respective `docs/protocol/search_string_*.md` files. Present at least the PubMed string in full in a supplementary table/box; the others can go in supplementary material. | ___ |
| 9 | Selection of sources of evidence — process for selecting sources (screening and eligibility). | Yes (content ready) | Title/abstract screening: Rayyan, single reviewer, sensitivity-favoring 3-gate criteria (`docs/protocol/screening_criteria.md`), TA-E1–E5 exclusion taxonomy. Full-text screening: F1-F5 criteria + E1-E6 exclusion taxonomy (`docs/protocol/screening_fulltext_criteria.md` v1.1). **Sole-reviewer status** at both T/A and full-text stages, faculty-confirmed accommodation given supervisor availability constraints (`memos/decision_log.md`, "Faculty adjudication delegated" and 2026-07-10 entries) — state this plainly as a disclosed deviation from the two-independent-reviewer standard. | ___ |
| 10 | Data charting process — methods used to chart data (forms, independent/duplicate charting, process for confirming data with investigators). | Yes | Methods, "Data extraction" (`manuscript_v1.md`); full column definitions in Supplementary Material S3. Charting was completed for all 7 included studies (`data/extraction/schema_v1.csv`). **Sole reviewer, no independent duplicate charting** — disclosed explicitly in Methods, "Limitations acknowledged in the design," as a departure from dual-reviewer convention rather than implied as duplicate charting. | ___ |
| 11 | Data items — list and define all variables sought, with assumptions/simplifications. | Yes | Full column definitions in Supplementary Material S3: clinical domain, XAI method/scope, study design/participants, evaluation type (six-level taxonomy), workflow realism, 4-dimension ecological validity, clinician involvement (evaluation vs. design, kept separate by design), outcomes claimed vs. demonstrated, trust-claim type (calibration vs. plausibility distinction), 5-dimension quality/risk-of-bias, method-justification type (RQ1), interpretability-framework classification (Doshi-Velez & Kim; Vilone & Longo), 4 regulatory-evidence criteria (RQ3), semantic tags. | ___ |
| 12 | Critical appraisal of individual sources of evidence — rationale, methods, and how used in synthesis (if done). | Yes (content ready) | Custom 5-dimension rubric (QR1-QR5: Participant Appropriateness, Task Fidelity, Outcome Measurement, Explanation Faithfulness, Reporting Completeness — `data/coding/quality_rubric.md`), adapted from QUADAS-2/RoB 2/TRIPOD elements plus two dimensions with no standard-tool equivalent (rationale: `memos/decision_log.md`, 2026-05-26 entry). Used as a supplementary/exploratory characterization of the corpus, **not** as an inclusion/exclusion filter — state this explicitly to avoid the appraisal reading as a second screening pass. | ___ |
| 13 | Synthesis of results — methods for handling/summarizing charted data. | Yes (content ready) | Narrative synthesis organized by RQ1-RQ3 (JBI methodology, Peters et al. 2020; PRISMA-ScR, Tricco et al. 2018) — not confirmatory hypothesis testing. The originally-planned H1-H6 hypotheses and quality-rubric scores are repositioned as supplementary/exploratory analyses feeding the RQ2 narrative, not primary confirmatory tests (2026-06-10 pivot decision). | ___ |

## Results

| # | Item | Reported? | Location / Notes | Page # |
|---|------|-----------|-------------------|--------|
| 14 | Selection of sources of evidence — numbers screened/assessed/included, reasons for exclusion at each stage, ideally a flow diagram. | Yes | Methods, "Study selection" (`manuscript_v1.md`): 659 identified (497 PubMed + 161 IEEE + 1 ACM) → 650 after deduplication → 650 screened at T/A → 64 forwarded to full-text → 55 assessed at full-text (9 not retrievable, disclosed separately from exclusions) → 48 excluded (E1=22, E2=5, E3=13, E4=8, E5=0, E6=0) → 7 included. The 2026-07-14 post-hoc differential-search supplement (46 additional candidates screened, 0 added) is reported alongside. Flow diagram built (`docs/figures/prisma_scr_flow_diagram.html`); convert to a static figure image at final typesetting. | ___ |
| 15 | Characteristics of sources of evidence — present charted characteristics per source, with citations. | Yes | Per-study characteristics charted in Tables 1-3 (`data/synthesis/results_tables_v1.md`) and full per-paper detail in `data/extraction/schema_v1.csv` / `data/extraction/per_paper/`; citations in `references_included_studies.md` (7 entries, DOI-verified). | ___ |
| 16 | Critical appraisal within sources of evidence — present appraisal data (if done). | Yes | QR1-QR5 scores charted per included paper in `data/extraction/schema_v1.csv`; referenced narratively in Results (e.g., Xie et al., 2021 scoring maximum on all five dimensions). Used as a supplementary/exploratory characterization, not an inclusion/exclusion filter (Methods, Data extraction). | ___ |
| 17 | Results of individual sources of evidence — relevant charted data per included source. | Yes | Per-paper extracted data (XAI method, eval type, realism level, trust claim, etc.) charted in `data/extraction/schema_v1.csv`; charted results presented in Tables 1-3 and synthesized narratively in Results (`manuscript_v1.md`). | ___ |
| 18 | Synthesis of results — summarize/present charting results as they relate to the review questions. | Yes | Results (`manuscript_v1.md`): "Methods and Justification (RQ1)," "Evaluation Rigor (RQ2)," "Regulatory Readiness (RQ3)" subsections, each a narrative synthesis of the charted data. | ___ |

## Discussion

| # | Item | Reported? | Location / Notes | Page # |
|---|------|-----------|-------------------|--------|
| 19 | Summary of evidence — main results (overview of concepts/themes/evidence types), link to questions/objectives, relevance to key groups. | Yes | Discussion (`manuscript_v1.md`), opening paragraph: summarizes the corpus-wide pattern (explanations built and computationally measured, but rarely evaluated with any human), links explicitly to RQ1-RQ3, and states relevance to the clinicians and regulatory audiences this review's findings address. | ___ |
| 20 | Limitations — discuss limitations of the scoping review process. | Yes | Methods, "Limitations acknowledged in the design," and Discussion, "What this corpus is small enough, and specific enough, to say" (`manuscript_v1.md`): Embase dropped (no institutional access); CINAHL shelved; English-language-only restriction; single reviewer with no independent duplicate screening/charting; 10 records never retrieved (9 main-corpus + 1 differential-supplement); small final corpus (n=7) framed as a substantive finding rather than an apology. | ___ |
| 21 | Conclusions — general interpretation relative to questions/objectives, implications, next steps. | Yes | Conclusion (`manuscript_v1.md`): interprets findings against RQ1-RQ3, states the review's contribution (governance-compliance standard for EM XAI evaluation), and closes on next steps (clinician-in-the-loop evaluation work this literature currently lacks). | ___ |

## Funding

| # | Item | Reported? | Location / Notes | Page # |
|---|------|-----------|-------------------|--------|
| 22 | Funding — sources of funding for included studies and for the review itself; role of funders. | Yes | **No funding was received for this review.** State this plainly in the manuscript's Funding/Declarations section (e.g., "This research received no specific grant from any funding agency in the public, commercial, or not-for-profit sectors."). | ___ |

---

## Completion Status Summary

All 22 items are reported as of 2026-07-26. Remaining work before submission is typesetting-dependent, not content-dependent:
- Fill in actual `Page #` values once the manuscript is typeset for a specific journal template.
- Convert the PRISMA-ScR flow diagram (`docs/figures/prisma_scr_flow_diagram.html`, Item 14) to a static figure image in the format the target journal requires.
- Verify item wording and section grouping against the official Tricco et al. (2018) checklist PDF before submission, per this document's standing verification note above.
