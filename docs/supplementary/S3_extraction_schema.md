# Supplementary Material S3: Data Extraction Schema — Full Column Definitions

Each of the 7 included studies was coded against a 43-column schema; the 42 analytically relevant columns are described below. (The schema's remaining column is an internal reference-manager lookup key with no analytic content and is not reported here.) Columns are grouped by theme; where a group maps to one of this review's three research questions, that mapping is noted in the group heading.

---

## Identity

| Column | Type | Description |
|--------|------|-------------|
| `PaperID` | string | Short identifier: `LASTNAME_YEAR` (first author only). |
| `Title` | string | Full paper title, copied verbatim. |
| `Year` | integer | Year of publication. |

---

## Clinical Domain

| Column | Type | Controlled vocabulary |
|--------|------|-----------------------|
| `Domain` | categorical | `Radiology` / `EHR` / `Pathology` / `ICU` / `Pharmacy` / `Oncology` / `Cardiology` / `Other` |

Coded as the primary clinical domain the AI system targets; `EHR` covers general inpatient/outpatient prediction using electronic health record data where no more specific specialty label applies.

---

## XAI Method and Scope

| Column | Type | Controlled vocabulary |
|--------|------|-----------------------|
| `XAI_Method` | categorical | `SHAP` / `LIME` / `GradCAM` / `Attention` / `ANCHOR` / `Counterfactual` / `Prototype` / `RuleExtraction` / `Other` / `Multiple` |
| `XAI_Scope` | categorical | `Local` / `Global` / `Both` |

`XAI_Scope` is coded as the method was actually used in the paper, not as the method is theoretically capable of. Attention weights are not coded as demonstrating a faithful explanation without additional evaluation evidence.

---

## Study Design and Participants

| Column | Type | Controlled vocabulary / Notes |
|--------|------|-------------------------------|
| `Study_Design` | categorical | `RCT` / `Observational` / `UserStudy` / `Simulation` / `MethodPaper` |
| `N_Participants` | integer | Number of human participants in the XAI evaluation specifically (not the model's training sample size); `0` if proxy metrics only. |
| `Participant_Type` | categorical | `None` / `LayPerson` / `ClinicalTrainee` / `Clinician` / `MixedClinical` |

`MethodPaper` denotes a paper whose stated primary contribution is the explanation method itself, using a clinical domain only as a demonstration case, with no systematic evaluation of clinical utility (see Supplementary Material S2, Criterion 3 exception).

---

## Evaluation Type (RQ2)

| Column | Type | Values |
|--------|------|--------|
| `Eval_Type` | categorical, multi-code | `ProxyMetric` / `ForwardSim` / `BackwardSim` / `TrustQuestionnaire` / `DecisionQuality` / `DownstreamOutcome` / `None` |

All evaluation types present in a paper are coded, semicolon-separated, ordered from lowest to highest ecological validity (e.g., `ProxyMetric; TrustQuestionnaire; DecisionQuality`). `None` is entered only when the paper presents an XAI system with no evaluation component at all. Definitions of each of the six levels are given in Supplementary Material S2, Criterion 3.

---

## Workflow Realism (RQ2)

| Column | Type | Values |
|--------|------|--------|
| `Realism_Level` | ordinal | `0` = No evaluation / `1` = Synthetic / `2` = Simulated / `3` = Ecologically representative / `4` = Deployment-embedded |
| `Realism_Notes` | string | Rationale for boundary-case coding decisions. |

---

## Ecological Validity (RQ2)

Each dimension is scored independently of the others.

| Column | Type | Values | Dimension |
|--------|------|--------|-----------|
| `EV_Participant` | ordinal 0-3 | 0=None / 1=NonClinician / 2=ClinOutOfRole / 3=ClinInRole | Participant validity |
| `EV_Task` | ordinal 0-3 | 0=NoTask / 1=Artificial / 2=Simplified / 3=FullyRepresentative | Task validity |
| `EV_Environment` | ordinal 0-3 | 0=NoInterface / 1=CustomResearch / 2=ClinicalLike / 3=ActualClinical | Environment validity |
| `EV_Outcome` | ordinal 0-3 | 0=NoneOrProxy / 1=SelfReport / 2=DecisionQuality / 3=PatientOutcomes | Outcome validity |
| `EV_Notes` | string | Boundary calls and mixed-participant-pool documentation. |

A composite score (sum of all four dimensions, range 0-12) is computed at analysis time rather than stored as its own column, since the four-dimension profile itself is the unit of analysis.

---

## Clinician Involvement

Involvement in evaluating the XAI system and involvement in designing it are recorded separately, since a study can involve clinicians in one role without the other.

| Column | Type | Values | Definition |
|--------|------|--------|------------|
| `Clinician_Eval` | boolean | `Yes` / `No` | Was a licensed clinician involved at any stage of evaluating the XAI system? |
| `Clinician_Role` | categorical, multi-code | `Rater` / `CoDesigner` / `EndUser` / `None` | Role of the clinician in the evaluation; `None` if `Clinician_Eval = No`. |
| `Clinician_Design` | boolean | `Yes` / `No` | Was a clinician involved in designing or developing the XAI system itself? |

---

## Outcomes and Trust

| Column | Type | Description |
|--------|------|-------------|
| `Outcome_Claimed` | string | What the paper states it demonstrates, quoted or closely paraphrased. |
| `Outcome_Demonstrated` | string | What is actually measured with a validated instrument, comparison condition, and appropriate sample size; blank if nothing is formally demonstrated. |
| `Trust_Claim` | categorical | `None` / `Calibrated` / `Plausibility` / `Both` |
| `Trust_Only` | boolean | `Yes` if a trust questionnaire is the sole evaluation of the XAI component present. |

`Trust_Claim` distinguishes a claim that an explanation helps a user calibrate trust to the system's actual reliability (`Calibrated`) from a claim or demonstration that an explanation is merely found convincing or satisfying, without evidence of calibration (`Plausibility`). This distinction underlies this review's trust-calibration-versus-plausibility construct (see Introduction).

---

## Quality and Risk of Bias

Each dimension is scored independently, adapted from QUADAS-2, RoB 2, and TRIPOD elements. This rubric characterizes methodological execution quality and is conceptually distinct from the ecological-validity dimensions above, which characterize evaluation realism.

| Column | Type | Values | Dimension |
|--------|------|--------|-----------|
| `QR_Participant` | ordinal 0-2 | 0=Inappropriate / 1=PartiallyAppropriate / 2=Appropriate | Participant appropriateness |
| `QR_Task` | ordinal 0-2 | 0=Misaligned / 1=PartiallyAligned / 2=WellAligned | Task fidelity |
| `QR_Outcome` | ordinal 0-2 | 0=InappropriateOrUnvalidated / 1=PartiallyValid / 2=ValidAndAppropriate | Outcome measurement validity |
| `QR_Faithfulness` | ordinal 0-2 | 0=None / 1=Indirect / 2=Direct | Explanation faithfulness |
| `QR_Reporting` | ordinal 0-2 | 0=MajorGaps / 1=Partial / 2=Complete | Reporting completeness |
| `QR_Notes` | string | Supporting detail for each dimension's score. |

A composite score (sum of all five dimensions, range 0-10) is computed at analysis time rather than stored as its own column.

---

## Method Justification (RQ1)

| Column | Type | Values | Definition |
|--------|------|--------|------------|
| `Method_Justification_Type` | categorical | `Computational` / `Cognitive` / `Workflow` / `Mixed` / `NotReported` | Why the paper says it chose its explanation method over alternatives |
| `Method_Justification_Notes` | string | — | Quote or close paraphrase of the stated justification |

Categories were coded inductively rather than as a closed a priori taxonomy: `Computational` covers justification on grounds such as model-agnosticism or theoretical guarantees; `Cognitive` covers justification on human-comprehensibility grounds; `Workflow` covers justification on deployment/integration grounds; `Mixed` records more than one type explicitly given; `NotReported` records the absence of any stated rationale, without inferring one the paper does not state.

---

## Method-Interface Isolation (RQ1/RQ2)

| Column | Type | Values | Definition |
|--------|------|--------|------------|
| `Method_Interface_Isolated` | categorical | `Yes` / `No` / `NotApplicable` | Does the study design allow an observed effect to be attributed to the explanation method itself, separate from how it is displayed? |

`Yes` requires a design that isolates method from presentation (e.g., multiple methods shown through an identical interface). `No` denotes a single method shown through a single interface with no comparison condition, leaving any effect on comprehension or trust confounded with presentation choices. `NotApplicable` denotes no human-facing interface exists at all.

---

## Framework Classification (RQ2/RQ3)

| Column | Type | Values |
|--------|------|--------|
| `DoshiVelez_Category` | categorical | `FunctionallyGrounded` / `HumanGrounded` / `ApplicationGrounded` |
| `VilonLongo_Category` | categorical | `Objective` / `HumanCentred_Qualitative` / `HumanCentred_Quantitative` / `HumanCentred_Mixed` / `NotEvaluated` |

`DoshiVelez_Category` follows Doshi-Velez and Kim's (2017) three-tier evaluation-grounding framework: `FunctionallyGrounded` denotes no human subjects, interpretability assessed via a formal proxy; `HumanGrounded` denotes human subjects performing a simplified or proxy task rather than the real target decision; `ApplicationGrounded` denotes real end-users performing the real target task in a realistic setting.

`VilonLongo_Category` follows Vilone and Longo's (2021) primary classification of evaluation approaches as objective/automated versus human-centred, with human-centred evaluations further split into qualitative (open-ended) and quantitative (close-ended) methods. This axis is independent of `DoshiVelez_Category`: the two frameworks classify different properties of an evaluation (how grounded/realistic it is, versus whether and how it involves humans) and are coded independently from the paper's actual method, not from one another.

---

## Regulatory-Relevant Evidence (RQ3)

Operationalizes what evidence would satisfy interpretability-validation expectations emerging in FDA AI/ML-based Software as a Medical Device guidance and EU AI Act Article 13.

| Column | Type | Values | Criterion |
|--------|------|--------|-----------|
| `Reg_Comprehension` | boolean | `Yes` / `No` | Clinician comprehension of explanation outputs, demonstrated via a comprehension check or correct-interpretation task |
| `Reg_TrustCalibration` | boolean | `Yes` / `No` | Trust shown to track actual model reliability across varying performance conditions |
| `Reg_UncertaintyTransparency` | boolean | `Yes` / `No` | Model uncertainty or failure modes surfaced to the clinician at the point of use, not merely discussed as a limitation |
| `Reg_WorkflowSafety` | boolean | `Yes` / `No` | Safe and effective use demonstrated within a realistic clinical workflow |
| `Reg_Notes` | string | — | Evidence supporting each `Yes`; for `No`, whether the criterion was addressed at all or attempted but insufficient |

All four criteria default to `No` in the absence of explicit, demonstrated evidence; a paper's stated future-work intentions or implications are not sufficient grounds for a `Yes` code.

---

## General Notes and Semantic Tags

| Column | Type | Description |
|--------|------|-------------|
| `Notes` | string | Free-text documentation of borderline coding decisions and details not captured by other columns. |
| `Tags` | string, multi-tag | Semicolon-separated semantic tags from a controlled vocabulary, supporting cross-cutting retrieval across papers (e.g., `#trust_calibration;#clinician_study;#deployment`). |
