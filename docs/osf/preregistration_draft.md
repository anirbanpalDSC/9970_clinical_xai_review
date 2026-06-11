# OSF Pre-Registration Draft - Explainable AI in Emergency Department Triage and Disposition: A Scoping Review (9970)

**Title:** Beyond Fidelity: Evaluating the Validity of Explainable AI in Emergency Department Triage and Disposition - A Scoping Review (PRISMA-ScR)
**Date drafted:** 2026-05-24
**Revised:** 2026-06-10 (pivot back to original proposal scope - EM/ED-only)
**Status:** Draft - for OSF update before search execution
**Contributors:** Anirban Pal
**OSF project:** https://osf.io/e3ymp/files/3f4am
**Registration:** OSF (primary, filed 2026-05-24, update pending). PROSPERO (Issue #19) deprioritised - see `docs/osf/prospero_draft.md`.
**Methodology:** JBI scoping review methodology (Peters et al., 2020) + PRISMA-ScR reporting (Tricco et al., 2018). Narrative synthesis - not confirmatory hypothesis testing.


## 1. Background and Rationale

Explainable AI (XAI) systems are increasingly proposed for emergency department (ED) decision support - including initial patient intake, acuity/triage scoring (e.g., the Emergency Severity Index, ESI), and immediate disposition decisions - on the premise that explanations help clinicians understand, calibrate trust in, and appropriately act on model outputs under severe time and cognitive constraints.

This review organises these claims under an **interpretability validity** framework spanning three constructs:

- **Interpretability** - the degree to which an explanation supports clinician understanding and decision-making under ED time/cognitive constraints.
- **Trust calibration** - alignment between clinician reliance on model outputs and the model's actual performance, avoiding over-trust and under-trust. This review applies a sharper distinction, developed during the protocol-design phase (`memos/conceptual_distinctions.md`, Issue #3), between trust calibration and **explanation plausibility**: a paper can demonstrate that an explanation *looks* convincing without demonstrating that clinician trust actually tracks model accuracy.
- **Evaluation validity** - the extent to which a study's design establishes a credible link between explanation outputs and downstream human decision behaviour. This review applies the 4-dimension ecological validity rubric (`EV_Participant` / `EV_Task` / `EV_Environment` / `EV_Outcome`, `data/coding/ecological_validity_rubric.md`, Issue #5) as a more granular operationalisation of this construct than a single undifferentiated "evaluation validity" dimension.

**Interpretability validity** is the extent to which evaluation practices in EM clinical XAI provide credible evidence that explanations are meaningful, usable, and appropriately calibrate clinician trust in real ED decision-making.

This review is scoped to the **initial ED encounter** - patient intake, acuity/triage scoring, and immediate disposition decisions - per `docs/protocol/inclusion_boundary.md` (v2). It is intended as scaffolding for empirical, clinician-in-the-loop studies planned in later phases of this research program.


## 2. Review Questions

**RQ1 - Methods and justification:** Which post-hoc explanation methods (feature attribution, counterfactual, example-based, rule-based) are deployed in EM clinical XAI studies, and what forms of justification - coded inductively as computational, cognitive, or workflow-based - are provided for their selection?

**RQ2 - Evaluation rigor:** How do current clinical XAI studies in EM evaluate explanation effectiveness across levels of human involvement (computational metrics, proxy tasks, simulated users, clinician-in-the-loop experiments, real-world deployment), and what does this distribution reveal about the rigor of existing evaluation practices?

**RQ3 - Regulatory readiness:** What evaluation evidence do current EM-focused XAI studies provide that would satisfy interpretability-validation expectations emerging in regulatory frameworks (FDA AI/ML-based Software as a Medical Device guidance; EU AI Act Article 13), and where are the most consequential evidentiary gaps?

"Regulatory-relevant evidence" (RQ3) is operationalised as evaluation demonstrating at least one of:
1. Clinician comprehension of explanation outputs;
2. Appropriate trust calibration under varying model performance conditions;
3. Transparency of model uncertainty / failure modes;
4. Safe and effective use within realistic clinical workflows.

These four criteria map directly to the `Reg_Comprehension`, `Reg_TrustCalibration`, `Reg_UncertaintyTransparency`, and `Reg_WorkflowSafety` extraction columns (Section 6).


## 3. Eligibility Criteria

Per the three-gate EM-only inclusion boundary in `docs/protocol/inclusion_boundary.md` (v2, revised 2026-06-10):

### Inclusion

- **Population/Context (Gate 1):** Adult or pediatric studies evaluating predictive models used for decisions occurring during the **initial ED encounter** - initial patient intake, acuity/triage scoring (e.g., ESI or an equivalent acuity scale), or immediate disposition (admit/discharge/transfer/ICU-admit) decisions made at the point of ED care.
- **Intervention (Gate 2):** A post-hoc explanation method (feature attribution, counterfactual, example-based/case-based, or rule-based) applied to the predictive model, OR an inherently interpretable model explicitly evaluated for its interpretability.
- **Study types (Gate 3):** Any empirical study reporting at least one of the five RQ2 evaluation levels (computational/fidelity, proxy task, simulated user, clinician-in-the-loop, deployment). Method papers presenting a novel XAI method with an EM clinical demonstration are eligible and coded `Study_Design: MethodPaper`.
- **Publication period:** 2015-2024 (inclusive) for the initial search. A search update covering January 2025 onward will be conducted shortly before manuscript submission (see `docs/protocol/search_string_pubmed_v1.md`).
- **Language:** English.

### Exclusion

- Models whose primary decision point occurs **outside** the initial ED encounter - pre-hospital EMS triage, inpatient ward monitoring, or ICU management - even if the study population originates in the ED (Gate 1).
- Operational/administrative ED models (crowding, throughput, staffing) with no patient-level intake/acuity/disposition decision (Gate 1).
- Predictive models with no interpretability/explanation component (Gate 2).
- Review articles, editorials, commentaries, opinion pieces, and protocol-only papers with no underlying empirical study (Gate 3); conference abstracts without full-text proceedings.

Full decision rule, decision flowchart, and 12 worked edge cases (including the decision-point-vs-population-origin distinction) are in `docs/protocol/inclusion_boundary.md`.


## 4. Databases and Search

Primary databases (per the original proposal): **PubMed/MEDLINE, Embase, IEEE Xplore, ACM Digital Library** (4 databases). CINAHL, included during the exploratory cross-domain phase, is shelved as a primary source under the EM-only scope (`memos/decision_log.md`, 2026-06-10) and may be used as a Phase 3 sensitivity check if time allows.

PubMed search string (Concept A: XAI/interpretability terms, AND Concept C: ED/triage/ESI/acuity/disposition terms) is documented in `docs/protocol/search_string_pubmed_v1.md`. The EM-narrowed v2 draft returns 234 hits (2015-2024, English) - down from 9,672 for the cross-domain v1 rev 3 string - pending finalisation (A+C vs A+B+C) and an EM-specific recall benchmark. Embase/IEEE/ACM translations (Issue #22) will be re-derived from this v2 string once finalised.

### Supplementary search

- **Google Scholar:** forward and backward citation tracing of *included* studies (conducted after full-text review), plus grey literature / preprint discovery (arXiv, SSRN).
- **Elicit:** semantic natural-language search per research question (RQ1-RQ3), with queries, dates, and result counts logged.
- **Provenance tracking:** each included study is tagged with its discovery source (primary database vs. supplementary source).

Full plan to be documented in `docs/protocol/supplementary_search_plan.md` (to be created).


## 5. Screening

- **Tool:** Rayyan, for deduplication and title/abstract + full-text screening.
- **Title/abstract IRR:** 15% random re-screen after a 2-week washout period; intra-rater Cohen's kappa reported. Borderline cases escalated to the supervising faculty member for adjudication. Full criteria and EM-specific exclusion taxonomy to be documented in `docs/protocol/screening_criteria.md` (Issue #17, to be created).
- **Full-text screening:** against the three-gate inclusion boundary (`docs/protocol/inclusion_boundary.md` v2).

Note: the title/abstract-stage IRR design (intra-rater kappa, single reviewer with re-screen) is distinct from the extraction-stage IRR design (two reviewers, inter-rater kappa, Section 8).


## 6. Extraction Schema

Full schema documented in `data/extraction/schema_v1.csv` (v1.3, 43 columns) and `data/extraction/schema_README.md`.

### New columns added for the EM pivot (2026-06-10)

| Column | RQ | Role |
|--------|----|------|
| `Method_Justification_Type`, `Method_Justification_Notes` | RQ1 | Inductive coding of method-selection justification: Computational / Cognitive / Workflow / Mixed / NotReported |
| `Method_Interface_Isolated` | RQ1/RQ2 | Whether explanation-method effects are isolated from interface/presentation effects |
| `DoshiVelez_Category`, `VilonLongo_Category` | RQ2/RQ3 | Framework classification against Doshi-Velez & Kim (2017) and Vilone & Longo (2021); the Vilone & Longo controlled vocabulary will be finalised during the 5-paper extraction pilot (Section 8) |
| `Reg_Comprehension`, `Reg_TrustCalibration`, `Reg_UncertaintyTransparency`, `Reg_WorkflowSafety`, `Reg_Notes` | RQ3 | The four regulatory-relevant-evidence criteria (Section 2) |

### Retained columns from the exploratory phase (preserved as upgrades, see Section 7.4)

| Column | Role |
|--------|------|
| `Eval_Type` | RQ2 - 6-type evaluation taxonomy mapped to Doshi-Velez & Kim (2017)'s 3-category framework (`memos/research_master_memo.md`, Issue #8) |
| `Realism_Level`, `Realism_Notes` | RQ2 - workflow realism rubric (Issue #4) |
| `EV_Participant`, `EV_Task`, `EV_Environment`, `EV_Outcome`, `EV_Notes` | RQ2 (supplementary) - 4-dimension ecological validity rubric (Issue #5) |
| `Trust_Claim`, `Trust_Only` | RQ3 - trust calibration vs. explanation plausibility (Issue #3) |
| `QR_Participant` ... `QR_Reporting`, `QR_Notes` | Supplementary quality/risk-of-bias rubric (Issue #20) |
| `Tags` | 21-tag semantic vocabulary (Issue #13) |


## 7. Synthesis Plan

This review uses **narrative synthesis organised by research question** (JBI scoping review methodology, Peters et al. 2020; PRISMA-ScR reporting, Tricco et al. 2018) - not confirmatory hypothesis testing.

### 7.1 RQ1 - Methods and Justification

Charted table of XAI method families (feature attribution / counterfactual / example-based / rule-based / inherently interpretable) by frequency, year, and EM decision category (intake / acuity / disposition). Inductive thematic coding of `Method_Justification_Type` and `Method_Justification_Notes`, with representative quotations illustrating each justification category (computational, cognitive, workflow-based).

### 7.2 RQ2 - Evaluation Rigor

Distribution of `Eval_Type` / `DoshiVelez_Category` across the five evaluation levels, cross-tabulated with EM decision category and XAI method family. The 4-D ecological validity rubric and workflow realism rubric (Issues #4/#5) provide a secondary, more granular lens on the same question - e.g., among clinician-in-the-loop studies, what proportion also achieve `EV_Environment >= 2` (realistic ED workflow conditions)?

### 7.3 RQ3 - Regulatory Readiness

For each of the four regulatory-relevant-evidence criteria (`Reg_Comprehension`, `Reg_TrustCalibration`, `Reg_UncertaintyTransparency`, `Reg_WorkflowSafety`), report the proportion of included studies providing that form of evidence, and characterise the most consequential gaps with reference to FDA AI/ML guidance and EU AI Act Article 13. The trust-calibration-vs-plausibility distinction (`Trust_Claim`, `Trust_Only`) directly informs the `Reg_TrustCalibration` assessment.

### 7.4 Supplementary / Exploratory Analyses

The 6 hypotheses originally specified during the cross-domain protocol-design phase (`memos/synthesis_hypotheses.md`, H1-H6) are **repositioned as supplementary, exploratory analyses** feeding the RQ2 narrative synthesis - not pre-registered confirmatory tests with their own significance thresholds. Where the EM-narrowed corpus supports it (adequate cell counts), these analyses (e.g., H1's clinician-co-design vs. ecological-validity comparison, H3's trust-claim composition) are reported descriptively alongside the RQ1-RQ3 narrative, explicitly labelled exploratory. Where cell counts are inadequate, the analysis is omitted and the omission is documented per the Deviations Protocol (Section 9).

The 5-dimension QR1-QR5 quality/risk-of-bias rubric (Issue #20) similarly feeds a sensitivity check: the RQ2/RQ3 narrative is repeated restricted to studies with `QS_Total >= 7`, to assess whether quality moderates the findings.

Meta-analysis is not planned - not appropriate for a scoping review of heterogeneous evaluation designs.


## 8. Inter-Rater Reliability - Extraction

Before full extraction:
1. Two reviewers independently code 5 seed papers on all schema columns.
2. Calculate Cohen's kappa for each categorical/ordinal column.
3. Target: kappa > 0.70 on all columns before proceeding to full extraction.
4. Discrepancies resolved by discussion; resolution logged in `memos/decision_log.md`.

Seed paper selection: draw from included papers after full-text screening, spanning all three EM decision categories (intake / acuity / disposition) and at least two evaluation levels.

This protocol (two reviewers, inter-rater kappa, 5-paper pilot) is distinct from the title/abstract-screening IRR protocol (Section 5: 15% re-screen, intra-rater kappa, faculty adjudication, Issue #17).

Full protocol documented in `data/extraction/schema_README.md`.


## 9. Deviations Protocol

If any planned analysis (an RQ1-RQ3 charted table, or a supplementary H1-H6/QR analysis) cannot be conducted as specified - e.g., insufficient cell counts for a supplementary hypothesis, or a regulatory-evidence criterion never observed in the corpus - document the deviation in `memos/decision_log.md` before finalising that section of the synthesis. Report what *can* be concluded from the available data; do not silently drop a planned analysis.

Any deviation from this pre-registered plan will be disclosed in the Methods section of the manuscript.


## 10. Timeline

| Phase | Weeks | Activities |
|-------|-------|------------|
| Phase 1 | 1-3 | Protocol/registration finalisation (this pivot, OSF update); EM-narrowed search execution across 4 databases; Rayyan deduplication; title/abstract screening (incl. 15% re-screen IRR); 5-paper extraction pilot |
| Phase 2 | 4-6 | Full-text screening; full extraction; RQ1-RQ3 narrative synthesis; supplementary analyses; manuscript drafting begins |
| Phase 3 | 7-8 | Manuscript drafting/revision; PRISMA-ScR flow diagram; January-2025-onward search update; submission to faculty |


## 11. Related Protocol Documents

| Document | Purpose |
|----------|---------|
| `docs/protocol/inclusion_boundary.md` (v2) | EM-only three-gate inclusion decision rule (Issue #7) |
| `docs/protocol/search_string_pubmed_v1.md` | PubMed search string - Concept A/B/C, EM-narrowed v2 (Issues #15, #22) |
| `docs/protocol/xai_method_taxonomy.md` | XAI method controlled vocabulary (Issue #6) |
| `docs/protocol/screening_criteria.md` | Title/abstract screening criteria + IRR design (Issue #17) |
| `docs/protocol/supplementary_search_plan.md` | Rayyan/Elicit/Google Scholar/provenance plan (Issue #23) |
| `data/coding/workflow_realism_rubric.md` | Workflow realism rubric (Issue #4) |
| `data/coding/eval_type_taxonomy.md` | Evaluation type taxonomy (Issue #8) |
| `data/coding/ecological_validity_rubric.md` | Ecological validity rubric (Issue #5) |
| `data/extraction/schema_v1.csv` | Extraction schema v1.3 (Issue #10) |
| `memos/synthesis_hypotheses.md` | H1-H6, repositioned as supplementary (Issue #9) |
| `memos/conceptual_distinctions.md` | Trust calibration vs plausibility (Issue #3) |
| `memos/terminology_instability.md` | XAI terminology conflict log (Issue #2) |
| `memos/tag_vocabulary.md` | Semantic tag controlled vocabulary (Issue #13) |
| `memos/decision_log.md` | 2026-06-10 EM-pivot decision and all prior decisions |


## Version History

| Version | Date | Changes |
|---------|------|---------|
| Draft v1 | 2026-05-24 | Initial draft. Cross-domain scope, 6 confirmatory hypotheses. Pre-registered before search execution. |
| Draft v2 - EM pivot | 2026-06-10 | Reverted to original proposal scope: EM/ED-only (initial encounter - intake / acuity-ESI / immediate disposition), RQ1-RQ3 with regulatory framing (FDA AI/ML guidance, EU AI Act Article 13), JBI scoping review (Peters 2020) + PRISMA-ScR (Tricco 2018) methodology, narrative synthesis by RQ. H1-H6 and QR1-QR5 repositioned as supplementary/exploratory. Database scope reverted to 4 (PubMed/Embase/IEEE/ACM); CINAHL shelved. Extraction schema -> v1.3 (10 new columns). See `memos/decision_log.md`, 2026-06-10. |
