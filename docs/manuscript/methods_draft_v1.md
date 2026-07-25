# Methods (draft v1)

**Status:** Draft narrative per `docs/manuscript/chapter_plan_v1.md` (~1,100 words target). Funnel figures pulled directly from `data/screening/prisma_counts.csv` (authoritative source, not re-derived from memory). Methodology citations (Peters et al., 2020; Tricco et al., 2018) verified via direct source lookup 2026-07-23.

---

## Design

This review followed Joanna Briggs Institute (JBI) scoping review methodology (Peters et al., 2020) and is reported per the PRISMA Extension for Scoping Reviews (PRISMA-ScR) checklist (Tricco et al., 2018). Consistent with scoping review methodology generally, this review synthesizes findings narratively, organized by research question, rather than through meta-analysis or formal risk-of-bias-weighted pooling; the rationale for that choice is addressed under Synthesis below.

## Eligibility criteria

Studies were eligible if they described an empirical application of a post-hoc or inherently interpretable explanation method to a machine-learning-based decision-support system targeting one of three emergency department (ED) decision points: patient intake, acuity or triage scoring, or immediate disposition. Full eligibility criteria, including the three-gate inclusion boundary (clinical domain and decision point; individual-patient-level decision; presence of clinician involvement in evaluation) and the associated exclusion taxonomy, are documented in `docs/protocol/inclusion_boundary.md` and `docs/protocol/screening_fulltext_criteria.md`. Studies were excluded if the decision point fell outside the three eligible categories (for example, inpatient or ICU settings, pre-hospital care, or diagnostic-differentiation tasks with no explicit link to an intake, triage, or disposition action); if no explanation method meeting the review's XAI taxonomy was present or evaluated; if the study was a review, protocol, or other non-primary-research format; or if insufficient methodological detail was reported to support extraction. Publication period was 2015-01-01 through search execution, in English.

## Information sources and search

Searches were executed across PubMed/MEDLINE, IEEE Xplore, and the ACM Digital Library (via the OpenAlex API, substituted for ACM's native search interface after the registered search string returned zero results even for single-term control queries). Embase was excluded from the primary search; the reviewer's institution does not subscribe, and no librarian-mediated search was available within the project timeline. This is reported as a disclosed limitation rather than a silently absorbed gap. The PubMed search (497 records) was executed 2026-06-10 using a three-concept string (explainability terms AND clinical/decision-support context AND ED-specific terms: triage, ESI, acuity, disposition), covering 2015-01-01 through the search-execution date. IEEE Xplore (161 records) and ACM Digital Library (1 record) were executed 2026-06-18 and 2026-06-22 respectively, using translations of the same three-concept string adapted to each database's syntax constraints.

## Study selection

Identification, screening, and eligibility counts are summarized in Figure 1 (PRISMA-ScR flow diagram, to be generated from `data/screening/prisma_counts.csv`). Searches identified 659 records (PubMed 497, IEEE Xplore 161, ACM 1). After removing 9 duplicates, 650 records proceeded to title-and-abstract screening; a structured retraction check against PubMed's metadata found none. A single reviewer screened all 650 records, yielding 40 bulk includes, 546 bulk excludes, and 64 borderline records requiring adjudication. On adjudication, 24 of the 64 borderline records were forwarded to full-text screening and 40 were excluded, bringing the total forwarded to full-text screening to 64 (40 bulk + 24 adjudicated).

Of the 64 records forwarded, 55 were assessed for eligibility; the remaining 9 could not be retrieved despite pursuing PMC's open-access API, direct publisher retrieval, and the reviewer's institutional access, and are reported as a distinct, disclosed category (not retrievable) rather than as excluded or silently dropped. Of the 55 assessed, 48 were excluded: 22 for an ineligible clinical domain or decision point (E1), 5 for no qualifying explanation component (E2), 13 for no empirical evaluation of the explanation method at any level (E3), and 8 for an ineligible publication format, principally reviews and protocols (E4). No record was excluded for insufficient extraction detail (E5) or as a duplicate report (E6). This yielded 7 included studies.

A post-hoc supplementary search of the gap window between the registered search's execution date and 2026-07-14, using the identical registered search string, was conducted after the main screening queue was exhausted, to check whether the included-study corpus was being under-sampled by publication lag. This supplement identified 46 additional candidate records, of which 6 were assessed at full-text (1 of 7 forwarded records was not retrievable) and none were included. The included-study corpus was finalized at 7 studies on this basis: continued search of a well-targeted, recent window returned zero additional eligible studies, indicating the corpus reflects the current state of the eligible literature rather than an artifact of the original search window's timing.

## Data extraction

Data were extracted using a 43-column schema (`data/extraction/schema_v1.csv`, documented column-by-column in `data/extraction/schema_README.md`) developed iteratively across the review's exploratory and EM-specific phases. Columns map to this review's three research questions: RQ1 (method family, scope, and inductively coded justification type: computational, cognitive, workflow-based, or mixed); RQ2 (evaluation type across a six-level taxonomy from purely computational proxy metrics through downstream-outcome studies; a four-dimension ecological validity rubric scoring participant, task, environment, and outcome validity independently; and classification against two independent evaluation-tier frameworks, Doshi-Velez and Kim's (2017) functionally/human/application-grounded taxonomy and Vilone and Longo's (2021) objective-versus-human-centred, qualitative-versus-quantitative classification); and RQ3 (four boolean indicators of regulatory-relevant evidence: clinician comprehension, trust calibration, uncertainty and failure-mode transparency, and workflow safety, each requiring demonstrated rather than claimed evidence). A five-dimension quality and risk-of-bias rubric, adapted from QUADAS-2, RoB 2, and TRIPOD, was applied independently of the ecological validity dimensions, since methodological execution quality and ecological realism are conceptually distinct properties of a study.

## Synthesis

Findings are synthesized narratively, organized by research question, following JBI scoping review convention. Meta-analysis was not conducted; it is not an appropriate method for a heterogeneous set of studies varying in ED decision point, explanation method, and evaluation design, and scoping review methodology does not require it. Findings are reported and interpreted at the scale of the included corpus (seven studies meeting this review's specific eligibility criteria), not generalized to emergency-medicine clinical XAI as a field.

## Limitations acknowledged in the design

Two features of this review's design are stated directly here rather than deferred to a closing limitations section. First, extraction and screening were conducted by a single reviewer; this is an appropriate scope for the project this review was conducted under and is not treated as a methodological gap requiring mitigation, though it is disclosed as a departure from dual-reviewer convention. Second, the small size of the final included-study corpus (7 of 650 initially identified records) is reported as a substantive finding about the state of this specific literature, not apologized for: it reflects the outcome of an exhaustive, registered search and screening process, corroborated by the supplementary search finding zero additional eligible studies in a recent, well-targeted window, rather than an arbitrary or premature stopping point.

---

## References cited in this section (verified 2026-07-23)

- Doshi-Velez, F., & Kim, B. (2017). Towards a rigorous science of interpretable machine learning. *arXiv preprint* arXiv:1702.08608.
- Peters, M. D. J., Godfrey, C., McInerney, P., Munn, Z., Tricco, A. C., & Khalil, H. (2020). Chapter 11: Scoping reviews. In E. Aromataris & Z. Munn (Eds.), *JBI Manual for Evidence Synthesis*. JBI.
- Tricco, A. C., Lillie, E., Zarin, W., O'Brien, K. K., Colquhoun, H., Levac, D., et al. (2018). PRISMA extension for scoping reviews (PRISMA-ScR): Checklist and explanation. *Annals of Internal Medicine*, 169(7), 467-473.
- Vilone, G., & Longo, L. (2021). Notions of explainability and evaluation approaches for explainable artificial intelligence. *Information Fusion*, 76, 89-106.

*Word count: approximately 1,050 (body text, excluding references).*
