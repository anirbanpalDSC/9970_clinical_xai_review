# Extraction Schema — schema_v1.csv

**Issue:** #10 (v1–v1.2), EM pivot 2026-06-10 (v1.3)
**Status:** v1.3 columns fully documented and verified 2026-07-22 — all 43 columns ready to extract
**File:** `data/extraction/schema_v1.csv`

This document is the canonical reference for every column in the extraction schema. All coders must read this before extracting. Where a column maps to a rubric or taxonomy, that document takes precedence over this README for boundary cases.

---

## Deviations from Issue #10 spec

Two columns were modified after the rubrics were finalised. The rubric definitions take precedence:

| Issue #10 specified | Schema uses | Reason |
|---------------------|-------------|--------|
| `Workflow_Realism` (ordinal 1–4) | `Realism_Level` (ordinal 0–4) | Rubric uses `Realism_Level`; 0 added for method-only papers with no evaluation |
| `Ecological_Validity_Score` (single ordinal 0–4) | `EV_Participant`, `EV_Task`, `EV_Environment`, `EV_Outcome` (four separate 0–3 columns) | Issue #5 rubric explicitly rejected a composite score — the profile is the data; collapsing discards analytically important mixed profiles |
| `Clinician_Involved` (single boolean) | `Clinician_Eval` + `Clinician_Design` (two booleans) | Synthesis hypothesis requires distinguishing clinician involvement in *evaluation* from involvement in *design*; a single column cannot capture both |

---

## Column Reference

### Identity

| Column | Type | Description |
|--------|------|-------------|
| `PaperID` | string | Short identifier: `LASTNAME_YEAR` (e.g., `Lundberg_2017`). Use first author only. If two papers share the same identifier, append `a`/`b` (e.g., `Kim_2018a`). |
| `Title` | string | Full paper title, copied verbatim. Do not truncate. |
| `Year` | int | Year of publication (journal or conference proceedings). Use Zotero metadata as authority. |
| `Zotero_Key` | string | Zotero item key (8-character alphanumeric string from Zotero URL or API). Required for traceability back to the reference manager. |

---

### Clinical Domain

| Column | Type | Controlled vocabulary |
|--------|------|-----------------------|
| `Domain` | categorical | `Radiology` / `EHR` / `Pathology` / `ICU` / `Pharmacy` / `Oncology` / `Cardiology` / `Other` |

Code the primary clinical domain the AI system targets. If a paper spans multiple domains, code the dominant one and note alternatives in `Notes`. `EHR` covers general inpatient/outpatient prediction using electronic health record data where no more specific specialty label applies.

---

### XAI Method and Scope

Controlled vocabulary defined in `docs/protocol/xai_method_taxonomy.md`. Read that document for boundary cases before coding.

| Column | Type | Controlled vocabulary |
|--------|------|-----------------------|
| `XAI_Method` | categorical | `SHAP` / `LIME` / `GradCAM` / `Attention` / `ANCHOR` / `Counterfactual` / `Prototype` / `RuleExtraction` / `Other` / `Multiple` |
| `XAI_Scope` | categorical | `Local` / `Global` / `Both` |

- If a paper uses multiple methods, enter `Multiple` in `XAI_Method` and list all methods in `Notes`.
- Code `XAI_Scope` as used in the paper, not as the method is theoretically capable of.
- Attention weights: do not code as demonstrating faithful explanation without additional evaluation evidence. See taxonomy coding notes.

---

### Study Design and Participants

| Column | Type | Controlled vocabulary / Notes |
|--------|------|-------------------------------|
| `Study_Design` | categorical | `RCT` / `Observational` / `UserStudy` / `Simulation` / `MethodPaper` |
| `N_Participants` | int | Number of human participants in the XAI evaluation. Enter `0` if the evaluation involves no human participants (proxy metrics only). Do not include model training sample size. |
| `Participant_Type` | categorical | `None` / `LayPerson` / `ClinicalTrainee` / `Clinician` / `MixedClinical` |

`Study_Design` notes:
- `RCT`: randomised controlled trial, any design (parallel, crossover, cluster)
- `Observational`: prospective or retrospective cohort, case-control, cross-sectional — no randomisation
- `UserStudy`: controlled evaluation of XAI with human participants; includes vignette studies, think-aloud, A/B evaluation — primary purpose is evaluating the XAI, not a clinical intervention
- `Simulation`: evaluation using simulation methods (forward/backward simulation tasks) — see eval_type_taxonomy.md
- `MethodPaper`: paper presents the XAI method itself; clinical domain is used as a demonstration case only; no systematic evaluation of clinical utility

`Participant_Type` notes:
- `ClinicalTrainee`: medical students, residents, junior nurses — any clinical role where autonomous practice is not yet established
- `MixedClinical`: paper includes both clinicians and non-clinicians or multiple clinical roles — document breakdown in `Notes`

---

### Evaluation Type

Controlled vocabulary defined in `data/coding/eval_type_taxonomy.md`. Read that document for boundary cases and minimum requirements before coding.

| Column | Type | Values |
|--------|------|--------|
| `Eval_Type` | categorical (multi-code) | `ProxyMetric` / `ForwardSim` / `BackwardSim` / `TrustQuestionnaire` / `DecisionQuality` / `DownstreamOutcome` / `None` |

**Multi-coding:** Enter all types present, separated by semicolons, ordered lowest to highest ecological validity:
> `ProxyMetric; TrustQuestionnaire; DecisionQuality`

Enter `None` only if the paper presents an XAI system with no evaluation component.

---

### Workflow Realism

Rubric defined in `data/coding/workflow_realism_rubric.md`. Read that document for boundary decision rules and positive examples before coding.

| Column | Type | Values |
|--------|------|--------|
| `Realism_Level` | ordinal | `0` = No evaluation / `1` = Synthetic / `2` = Simulated / `3` = Ecologically representative / `4` = Deployment-embedded |
| `Realism_Notes` | string | Document: multi-component evaluations coded at highest level, ambiguous boundary calls, rationale for edge-case decisions |

---

### Ecological Validity

Rubric defined in `data/coding/ecological_validity_rubric.md`. Score each dimension independently before looking at the others.

| Column | Type | Values | Dimension |
|--------|------|--------|-----------|
| `EV_Participant` | ordinal 0–3 | 0=None / 1=NonClinician / 2=ClinOutOfRole / 3=ClinInRole | Participant validity |
| `EV_Task` | ordinal 0–3 | 0=NoTask / 1=Artificial / 2=Simplified / 3=FullyRepresentative | Task validity |
| `EV_Environment` | ordinal 0–3 | 0=NoInterface / 1=CustomResearch / 2=ClinicalLike / 3=ActualClinical | Environment validity |
| `EV_Outcome` | ordinal 0–3 | 0=NoneOrProxy / 1=SelfReport / 2=DecisionQuality / 3=PatientOutcomes | Outcome validity |
| `EV_Notes` | string | Mixed participant pools, boundary calls, inconsistencies with `Realism_Level` |

A composite EV score is not stored in the schema. Compute `EV_Participant + EV_Task + EV_Environment + EV_Outcome` (range 0–12) at analysis time if a summary measure is needed.

---

### Clinician Involvement

Two booleans — involvement in **evaluation** and in **design** — are kept separate because the synthesis hypotheses address both independently.

| Column | Type | Values | Definition |
|--------|------|--------|------------|
| `Clinician_Eval` | boolean | `Yes` / `No` | Was a licensed clinician involved at any stage of evaluating the XAI system? |
| `Clinician_Role` | categorical | `Rater` / `CoDesigner` / `EndUser` / `None` | Role of the clinician in the evaluation. `Rater` = judged explanation quality. `EndUser` = used XAI to make decisions. `CoDesigner` = contributed to evaluation design. Use `None` if `Clinician_Eval` = No. Multi-code with semicolons if multiple roles. |
| `Clinician_Design` | boolean | `Yes` / `No` | Was a clinician involved in designing or developing the XAI system (co-design, requirements elicitation, iterative feedback during development)? Code from the Methods section. |

---

### Outcomes

| Column | Type | Description |
|--------|------|-------------|
| `Outcome_Claimed` | string | What the paper states it demonstrates in the abstract, introduction, or conclusion. Quote or close paraphrase. |
| `Outcome_Demonstrated` | string | What is actually measured with a validated instrument, comparison condition, and appropriate sample size. Summarise what the data show, not what the authors claim. Leave blank if nothing is formally demonstrated. |
| `Trust_Claim` | categorical | `None` / `Calibrated` / `Plausibility` / `Both` |
| `Trust_Only` | boolean | `Yes` / `No` — enter `Yes` if a trust questionnaire is the **sole** evaluation of the XAI component. This flags papers that claim trust improvement with no supporting decision quality or outcome evidence. See terminology_instability.md Part 3 (Trust calibration ≠ Explanation plausibility). |

`Trust_Claim` codes:
- `None`: paper does not make a trust-related claim
- `Calibrated`: paper claims that the explanation helps users calibrate their trust (i.e., trust is proportional to actual system reliability)
- `Plausibility`: paper demonstrates or claims that clinicians find the explanation plausible or satisfying, without evidence of calibration
- `Both`: paper claims calibration but only demonstrates plausibility

---

### Quality and Risk of Bias

Rubric defined in `data/coding/quality_rubric.md`. Score each dimension independently before looking at others. Read that document for the standard tools mapping, boundary notes, and study-design-conditional scoring rules.

| Column | Type | Values | Dimension |
|--------|------|--------|-----------|
| `QR_Participant` | ordinal 0–2 | 0=Inappropriate / 1=PartiallyAppropriate / 2=Appropriate | Participant appropriateness — match between participant type and paper claims |
| `QR_Task` | ordinal 0–2 | 0=Misaligned / 1=PartiallyAligned / 2=WellAligned | Task fidelity — alignment between task design and stated research question |
| `QR_Outcome` | ordinal 0–2 | 0=InappropriateOrUnvalidated / 1=PartiallyValid / 2=ValidAndAppropriate | Outcome measurement — validity of instruments used |
| `QR_Faithfulness` | ordinal 0–2 | 0=None / 1=Indirect / 2=Direct | Explanation faithfulness — evidence that explanation reflects model behaviour |
| `QR_Reporting` | ordinal 0–2 | 0=MajorGaps / 1=Partial / 2=Complete | Reporting completeness — XAI method, model, dataset, evaluation procedure |
| `QR_Notes` | string | Mandatory-field gaps (QR_Reporting=0), instrument name and citation (QR_Outcome), faithfulness method (QR_Faithfulness=2) | Free text |

A composite quality score (QS_Total = sum of all five QR columns, range 0–10) is not stored in the schema — compute at analysis time.

**Key distinction from EV columns:** EV dimensions characterise the ecological validity of the evidence (what was studied and how realistic it was). QR dimensions assess whether the study executed its design well (methodological quality). These are independent — see cross-reference table in `data/coding/quality_rubric.md` Section 6.

---

### General Notes

| Column | Type | Description |
|--------|------|-------------|
| `Notes` | string | Free text. Use for: method breakdown when `XAI_Method=Multiple`, domain breakdown when multiple domains apply, flags for second reviewer, borderline coding decisions not covered by other note fields, links to decision log entries. |

---

### Semantic Tags

Controlled tag vocabulary defined in `memos/tag_vocabulary.md`. Read that document before applying tags.

| Column | Type | Description |
|--------|------|-------------|
| `Tags` | string (multi-tag) | Semicolon-separated list of semantic tags from the controlled vocabulary in `memos/tag_vocabulary.md`. Example: `#trust_calibration;#clinician_study;#deployment`. Apply all tags that meet the `When to use` condition — no minimum, no maximum. Tags must appear in the controlled vocabulary; propose new tags in `memos/decision_log.md` before use. |

Tags that overlap with categorical schema columns (e.g., `#trust_calibration` mirrors `Trust_Claim: Calibrated`) should still be populated in both places — the Tags column enables memo-level cross-cutting retrieval that schema filters alone do not support.

---

### Method Justification (RQ1)

Inductive coding — categories below are starting definitions, not a closed a priori taxonomy. Refine wording in `Method_Justification_Notes` as coding proceeds; if a genuinely new justification type emerges across the 7 papers, log it in `memos/decision_log.md` before treating it as a category.

| Column | Type | Values | Definition |
|--------|------|--------|------------|
| `Method_Justification_Type` | categorical | `Computational` / `Cognitive` / `Workflow` / `Mixed` / `NotReported` | Why the paper says it chose this XAI method over alternatives |
| `Method_Justification_Notes` | string | — | Quote or close paraphrase of the justification, with page/section reference |

`Method_Justification_Type` codes:
- `Computational`: justified on computational grounds — model-agnosticism, speed, compatibility with the model architecture, established benchmark performance, theoretical guarantees (e.g., Shapley additivity)
- `Cognitive`: justified on human-comprehensibility grounds — alignment with clinical reasoning, simplicity of the explanation form, prior evidence the format is understandable
- `Workflow`: justified on deployment/integration grounds — fits existing clinical tools, low latency for ED use, compatibility with EHR display constraints
- `Mixed`: paper gives more than one of the above explicitly — record all applicable types in `Notes`, primary type in this column
- `NotReported`: method is used with no stated rationale for why it was chosen over alternatives (the common case — do not infer a justification the paper doesn't state)

---

### Method-Interface Isolation (RQ1/RQ2)

| Column | Type | Values | Definition |
|--------|------|--------|------------|
| `Method_Interface_Isolated` | categorical | `Yes` / `No` / `NotApplicable` | Does the study design let you attribute an observed effect to the explanation *method* itself, separate from how it's displayed? |

- `Yes`: design isolates the method from presentation — e.g., compares multiple XAI methods through an identical interface, or explicitly varies interface while holding method constant and analyzes the two effects separately
- `No`: a single method is shown through a single interface with no comparison condition — any effect on comprehension/trust/decision quality is confounded between "the explanation method" and "the way it happened to be displayed"
- `NotApplicable`: no human-facing interface exists (e.g., `MethodPaper` with only computational/proxy evaluation, `Eval_Type = None`)

This is the RQ1/RQ2 cross-cutting flag: a paper can score well on `Eval_Type`/`Realism_Level` while still leaving method and interface effects confounded — worth checking for every `UserStudy`/`RCT`/`Observational` row.

---

### Framework Classification (RQ2/RQ3)

| Column | Type | Values | Definition |
|--------|------|--------|------------|
| `DoshiVelez_Category` | categorical | `FunctionallyGrounded` / `HumanGrounded` / `ApplicationGrounded` | Doshi-Velez & Kim (2017) 3-category evaluation framework |
| `VilonLongo_Category` | categorical | **interim — see caveat below** | Vilone & Longo (2021) evaluation-approach classification |

**`DoshiVelez_Category` coding rules** (Doshi-Velez & Kim, 2017, "Towards a Rigorous Science of Interpretable Machine Learning"):
- `FunctionallyGrounded`: no human subjects; interpretability assessed via a formal proxy (fidelity metric, sparsity, a previously-validated proxy task) — maps to `Eval_Type = ProxyMetric` and `N_Participants = 0`
- `HumanGrounded`: human subjects perform a simplified or proxy task, not the real target decision (e.g., forced-choice explanation comparison, forward/backward simulation, or a trust/utility questionnaire completed as an assigned task by independent participants) — maps to `Eval_Type` containing `ForwardSim`/`BackwardSim`/`TrustQuestionnaire` without `DecisionQuality`/`DownstreamOutcome`. `TrustQuestionnaire` lands here (not `FunctionallyGrounded`) whenever real, independent human participants completed an assigned survey task, even if the instrument itself is unvalidated — distinct from the `Eval_Type=None` + `N_Participants>0` tie-break above, which covers informal, task-less, non-independent commentary (e.g. a co-author glancing at a couple of examples).
- `ApplicationGrounded`: real end-users (ideally clinicians) perform the real target task in a realistic setting — maps to `Eval_Type` containing `DecisionQuality` or `DownstreamOutcome` combined with `EV_Task >= 2` and `EV_Participant >= 2`

Coding `DoshiVelez_Category` should be a near-mechanical function of `Eval_Type` + `EV_Participant` + `EV_Task` already recorded — if the two disagree, treat it as a flag for `Notes`, not a silent overwrite of either column.

**Tie-break (decision log 2026-07-23, added after `Arnaud_2023`):** when `Eval_Type = None` (no evaluation activity meets any taxonomy minimum) but `N_Participants > 0` (an informal, non-systematic human involvement exists — e.g. a co-author's face-validity commentary on a couple of illustrative examples, with no assigned task and no independent/blinded participants), code `DoshiVelez_Category = FunctionallyGrounded` and flag it in `Notes`. This is a documented tie-break, not a claim the paper's evaluation is genuinely functionally-grounded in the textbook sense — none of the three buckets cleanly fits an informal, sub-taxonomy-threshold human review, and `FunctionallyGrounded` is the least-wrong label since neither `HumanGrounded` nor `ApplicationGrounded`'s criteria are met either.

**`VilonLongo_Category` — verified 2026-07-22 against the primary source** (Vilone & Longo, 2021, *Information Fusion* 76:89–106, DOI 10.1016/j.inffus.2021.05.009, Section 4 / Fig. 5 / Table 4, open access via `https://arrow.tudublin.ie/scschcomart/135/`).

An earlier draft of this section wrongly listed `ApplicationGrounded_RealUsers` / `HumanGrounded_ProxyTask` / `FunctionallyGrounded_ProxyMetric` / `FunctionallyGrounded_Simulation` — that was Doshi-Velez & Kim's grounding framework mislabeled as Vilone & Longo's, which would have made this column redundant with `DoshiVelez_Category`. Having now read the paper directly: Vilone & Longo's own primary classification (Section 4) is **Objective vs. Human-centred** evaluation — the grounding-based three-way split is explicitly presented in their paper as an *alternative* scheme from the literature (attributed there to [2], Preece 2018), not their own proposed category system. Human-centred evaluations are further split into **Qualitative** (open-ended questions/interviews) vs. **Quantitative** (close-ended — Likert scales, forced-choice accuracy, yes/no judgments), per their Table 4 classification of the 70 reviewed evaluation studies.

| Value | Definition |
|-------|------------|
| `Objective` | Evaluated using only automated/formal metrics, no human participants judging explanation quality — e.g., fidelity/infidelity, sensitivity to input or parameter perturbation, rule validity/redundancy percentages, text-quality metrics (BLEU/METEOR/CIDEr-style), productivity/performance indicators. Maps to `N_Participants = 0`. |
| `HumanCentred_Qualitative` | Human participants evaluate explanations via open-ended methods only (interviews, think-aloud, free-text feedback) — no Likert/close-ended instrument. |
| `HumanCentred_Quantitative` | Human participants evaluate explanations via close-ended methods only (Likert scales, forced-choice accuracy, timed tasks, yes/no judgments). |
| `HumanCentred_Mixed` | Paper combines both open- and close-ended human-centred measures (common in the reviewed literature — e.g., a Likert-scale questionnaire plus an open-ended interview in the same study). |
| `NotEvaluated` | No evaluation component. |

This axis is deliberately orthogonal to `DoshiVelez_Category`: Doshi-Velez asks how *realistic/grounded* the evaluation task is; `VilonLongo_Category` asks whether the evaluation was *automated, or human-centred and open- vs. closed-ended*. A paper can be, e.g., `ApplicationGrounded` + `HumanCentred_Quantitative` (real clinicians, real task, evaluated via Likert scale) — code both columns independently from the paper's actual method, not from each other.

No pilot needed before extracting this column — the vocabulary above is verified against the primary source, not provisional.

---

### Regulatory-Relevant Evidence (RQ3)

Maps to the four regulatory-relevant-evidence criteria defined in the preregistration (Section 2), operationalizing what evidence would satisfy interpretability-validation expectations in FDA AI/ML-based SaMD guidance and EU AI Act Article 13.

| Column | Type | Values | Criterion |
|--------|------|--------|-----------|
| `Reg_Comprehension` | boolean | `Yes` / `No` | Clinician comprehension of explanation outputs |
| `Reg_TrustCalibration` | boolean | `Yes` / `No` | Appropriate trust calibration under varying model performance conditions |
| `Reg_UncertaintyTransparency` | boolean | `Yes` / `No` | Transparency of model uncertainty / failure modes |
| `Reg_WorkflowSafety` | boolean | `Yes` / `No` | Safe and effective use within realistic clinical workflows |
| `Reg_Notes` | string | — | Cite the specific evidence supporting each `Yes`; if `No`, note whether the criterion was addressed at all vs. attempted but insufficient |

Coding rules:
- `Reg_Comprehension = Yes` requires the paper to *test* comprehension (e.g., a comprehension check, correct-interpretation task) — a clinician merely viewing the explanation does not qualify.
- `Reg_TrustCalibration = Yes` requires evidence trust tracked actual model reliability across varying performance conditions (e.g., trust measured against both correct and incorrect model outputs) — this is the calibration sense, not plausibility. Cross-check against `Trust_Claim`: a `Trust_Claim = Calibrated` or `Both` row is a candidate for `Yes`; `Trust_Claim = Plausibility` alone should be `No` here even if the paper frames it as a trust result.
- `Reg_UncertaintyTransparency = Yes` requires the explanation or system surfaces model uncertainty or failure conditions to the user (e.g., confidence scores, out-of-distribution flags, explicit "explanation may be unreliable when...") — not just that the paper *discusses* uncertainty as a limitation.
- `Reg_WorkflowSafety = Yes` requires evaluation within a realistic clinical workflow context — cross-check against `Realism_Level >= 3` and `EV_Environment >= 2`; a paper scoring low on those columns should not independently score `Yes` here without a specific justification recorded in `Reg_Notes`.
- All four default to `No` in the absence of explicit evidence — do not infer regulatory-relevant evidence from a paper's stated implications or future-work claims.

---

## Inter-Rater Reliability Protocol

Before full extraction begins:
1. Two reviewers independently code 5 seed papers on all columns.
2. Calculate Cohen's kappa for each categorical/ordinal column.
3. Target: κ > 0.70 on all columns before proceeding.
4. Discrepancies resolved by discussion; resolution logged in `memos/decision_log.md`.

Seed paper selection: draw from included papers after full-text screening is complete. Choose papers that span at least three different domains and two realism levels.

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1 | 2026-05-24 | Initial schema. 26 columns. Deviates from Issue #10 spec on `Realism_Level`, EV columns, and clinician involvement split — see Deviations section. |
| v1.1 | 2026-05-24 | Added `Tags` column (27 columns total). Issue #13. Controlled tag vocabulary in `memos/tag_vocabulary.md` (21 tags across 4 groups). |
| v1.2 | 2026-05-26 | Added 6 quality rubric columns: `QR_Participant`, `QR_Task`, `QR_Outcome`, `QR_Faithfulness`, `QR_Reporting`, `QR_Notes` (33 columns total). Issue #20. Rubric in `data/coding/quality_rubric.md`. Adopted and adapted from QUADAS-2, RoB 2, and TRIPOD — see rubric Section 2 for mapping. |
| v1.3 | 2026-06-10 (columns) / 2026-07-22 (documented) | Added 10 columns for the EM pivot's RQ1–RQ3 framework (43 columns total): `Method_Justification_Type`, `Method_Justification_Notes`, `Method_Interface_Isolated`, `DoshiVelez_Category`, `VilonLongo_Category`, `Reg_Comprehension`, `Reg_TrustCalibration`, `Reg_UncertaintyTransparency`, `Reg_WorkflowSafety`, `Reg_Notes`. Columns existed in the CSV since the 2026-06-10 pivot but were undocumented until now. `VilonLongo_Category` vocabulary verified 2026-07-22 directly against Vilone & Longo (2021) primary source (Objective / HumanCentred_Qualitative / HumanCentred_Quantitative / HumanCentred_Mixed / NotEvaluated) — ready to extract, no pilot required. |
