# Quality and Risk of Bias Assessment Rubric — Clinical XAI

**Issue:** #20
**Status:** Resolved 2026-05-26
**Feeds:** `QR_Participant`, `QR_Task`, `QR_Outcome`, `QR_Faithfulness`, `QR_Reporting` columns in extraction schema (v1.2)
**Cross-referenced:** `data/coding/ecological_validity_rubric.md` (Issue #5); `data/coding/eval_type_taxonomy.md` (Issue #8)

---

## 1. Purpose and Relationship to the Ecological Validity Rubric

The **ecological validity rubric** (Issue #5) characterises _what_ a study evaluated and _where_ it sits on the ecological validity spectrum — whether real clinicians, real tasks, real environments, and real outcomes were involved. It describes the study's validity profile without judging whether the study executed its design well.

The **quality rubric** asks a different question: _given what the study set out to do, did it do it well?_ A proxy-metric study at Realism Level 1 can still achieve high quality if it uses validated faithfulness metrics, reports all methods completely, and makes no unwarranted clinical claims. A user study with real clinicians can score low quality if its outcome measure is unvalidated, its XAI evaluation is unfaithful to the model, and key methods are unreported.

These rubrics are complementary, not redundant:

| Rubric | Question answered | Risk if omitted |
|--------|------------------|-----------------|
| Ecological validity (EV) | How ecologically valid is the evidence? | Synthesis cannot distinguish lab demonstrations from deployment evidence |
| Quality (QR) | How well was the study designed and reported? | Synthesis treats all included studies as equally reliable |

The five QR dimensions were selected to cover the primary methodological failure modes in clinical XAI evaluation papers, each distinct from what the EV rubric captures. The cross-reference table in Section 6 documents dimension-by-dimension overlap.

---

## 2. Standard Tools Review

Three established quality assessment tools were evaluated for applicability. Each was reviewed against the typical study designs found in clinical XAI evaluation papers (proxy-metric studies, user studies, simulation studies, deployment studies). Full rationale for adoption and rejection decisions is in `memos/decision_log.md` (2026-05-26 entry).

### QUADAS-2 (Quality Assessment of Diagnostic Accuracy Studies)

QUADAS-2 assesses four domains for diagnostic test accuracy studies: Patient Selection, Index Test, Reference Standard, Flow and Timing.

| Domain | Applicable to XAI? | Disposition |
|--------|-------------------|-------------|
| Patient Selection | Partially — selection bias in participant recruitment applies to XAI user studies | **Adapted** into QR1 (Participant Appropriateness) |
| Index Test | No — the "index test" concept (a diagnostic test with a threshold) does not map onto XAI evaluation. Blinding is structurally impossible in XAI user studies (participants see the explanation). | **Rejected** |
| Reference Standard | Yes — requires an independent reference against which the test is validated. Maps directly to the need for an independent ground truth against which explanation faithfulness is verified. | **Adapted** into QR4 (Explanation Faithfulness) |
| Flow and Timing | No — designed for studies where all patients receive both index test and reference standard; not applicable to XAI evaluation designs. | **Rejected** |

### RoB 2 (Risk of Bias in Randomised Trials, Cochrane)

RoB 2 assesses five domains specific to randomised trials.

| Domain | Applicable to XAI? | Disposition |
|--------|-------------------|-------------|
| D1 — Randomisation process | Rarely — fewer than 10% of XAI evaluation papers are RCTs (H5 hypothesis). | **Rejected** as a standalone domain; coded via `Study_Design: RCT` in schema |
| D2 — Deviations from intended intervention | Partially — did participants engage with the XAI component as described? Protocol fidelity is relevant but rarely reportable from paper text. | **Partially adopted** into QR2 (Task Fidelity) as "was the evaluation conducted as designed?" |
| D3 — Missing outcome data | Partially — attrition and exclusions in user studies. | **Absorbed** into QR5 (Reporting Completeness) |
| D4 — Measurement of outcome | Yes — were outcome measures validated and appropriate? Maps directly to clinical XAI evaluation. | **Adopted** as the foundation for QR3 (Outcome Measurement) |
| D5 — Selection of reported result | Yes — selective reporting of favourable evaluation results is a risk in XAI papers. | **Adopted** as a component of QR5 (Reporting Completeness) |

### TRIPOD (Transparent Reporting of Multivariable Prediction Models)

TRIPOD is a reporting guideline (not a risk of bias tool) for prediction model development and validation. It covers model specification, predictors, outcomes, sample size, performance reporting, and validation type.

| Element | Applicable to XAI? | Disposition |
|---------|-------------------|-------------|
| Model specification and predictors | Partially — the underlying model is background to the XAI evaluation but must be described for the explanation to be interpretable. | **Adopted** as a component of QR5 (Reporting Completeness) |
| Sample size and missing data | Partially — applies to the evaluation cohort, not just model training. | **Adopted** as a component of QR5 |
| Internal vs external validation type | Background only — relevant to the underlying model's reliability, not the XAI evaluation per se. | **Rejected** as a QR dimension; noted as a `Notes`-field flag where relevant |
| Calibration and discrimination | Not applicable — these are predictive model metrics, not XAI evaluation metrics. | **Rejected** |

### What the custom rubric adds beyond standard tools

Standard tools share a common gap: none was designed for evaluation of explanation methods. Three dimensions are entirely absent from QUADAS-2, RoB 2, and TRIPOD:
- **Explanation faithfulness** — whether the explanation accurately reflects model behaviour (not just whether outputs are plausible)
- **Participant-to-claim match** — whether participants are appropriate given what the paper claims, rather than just whether selection was unbiased
- **Reporting completeness for XAI** — whether the XAI method, not just the underlying model, is described with sufficient detail to replicate

---

## 3. The Five Quality Dimensions

Each dimension is scored **0–2**. Score the study as conducted, not as described. QR dimensions assess methodological quality of execution; EV dimensions assess ecological validity of context — score each independently.

---

### QR1 — Participant Appropriateness

**Question:** Are the study participants appropriate for the claims the paper makes about the XAI system?

This dimension assesses the match between who evaluated the XAI and what the paper claims its evaluation demonstrates. A paper claiming generalisability to clinical practice must involve clinicians in that practice domain. A paper explicitly scoped to a technical feasibility demonstration does not require clinical participants.

| Score | Label | Criteria |
|-------|-------|----------|
| 0 | Inappropriate | Participants are clearly mismatched to the paper's stated claims. Examples: lay participants or medical students used when the paper claims clinical utility for licensed practitioners; wrong clinical specialty when specialty-specific performance is claimed; animal or synthetic surrogate used when human decision impact is claimed. |
| 1 | Partially appropriate | Participants partially match the study's claims but with significant limitations not acknowledged by the authors. Examples: clinicians from a related but non-target specialty; mixed pool of appropriate and inappropriate participants with no sub-group analysis; convenience sample from a single institution with claims of broad generalisability. |
| 2 | Appropriate | Participants are well-matched to the study's stated claims and intended user population, OR the evaluation design does not involve human participants and the paper's claims are scoped accordingly (e.g., proxy-metric-only study claiming only technical properties of the XAI). |

**Boundary notes:**
- A proxy-metric study (no participants) claiming only "this method produces faithful explanations": QR1 = 2 (claims match design — no participant needed)
- A proxy-metric study claiming "this method will improve clinical decisions": QR1 = 0 (clinical claim with no clinical evaluation)
- A study with medical students where the paper explicitly scopes claims to understanding rather than clinical performance: QR1 = 2 (scope matches participants)

**Relationship to EV_Participant:** EV_Participant scores the type of participant (0–3: none → non-clinician → out-of-role → in-role). QR1 scores the match between participant type and the paper's claims. A study with EV_Participant = 1 (non-clinicians) can score QR1 = 2 if the paper's claims are appropriately scoped to non-clinical populations.

---

### QR2 — Task Fidelity

**Question:** Was the evaluation task designed to answer the paper's stated research question, and was it conducted as described?

This dimension assesses whether the task structure is internally coherent with the study's goals. A study asking whether clinicians comprehend XAI outputs appropriately might validly use a forward simulation task (which would score low on EV_Task but high on QR2 if comprehension is the stated RQ). A study claiming to test decision improvement must use a decision task.

| Score | Label | Criteria |
|-------|-------|----------|
| 0 | Misaligned | The evaluation task does not address the paper's stated research question. Examples: paper claims to improve clinical decision-making but measures only explanation preference ratings; paper claims to assess trust calibration but only asks whether explanations look plausible; task structure is logically inconsistent with the stated hypothesis. |
| 1 | Partially aligned | Task partially addresses the research question but with notable gaps. Examples: decision task used but no comparison condition (XAI vs no XAI) when an improvement claim is made; forward simulation task used when the RQ involves clinical workflow integration; paper acknowledges task limitations but draws strong conclusions anyway. |
| 2 | Well-aligned | The task structure directly addresses the stated research question. Comparison conditions match the hypothesis being tested. Stated limitations are appropriate in scope given the task. |

**Boundary notes:**
- Likert trust rating is task-aligned if the RQ is "do clinicians find these explanations trustworthy?" — but not if the RQ is "do explanations improve diagnostic accuracy"
- Forward/backward simulation tasks (EV_Task = 1) can score QR2 = 2 if the RQ is about cognitive comprehension of explanations
- A well-designed RCT with randomisation to XAI vs no XAI and a decision quality outcome would score QR2 = 2 even if the task is a simplified vignette (EV_Task = 2)

**Relationship to EV_Task:** EV_Task scores how representative the task is of real clinical practice (0–3: no task → artificial → simplified → fully representative). QR2 scores whether the task is appropriate for the stated research question. These are independent: a realistic task can be misaligned (QR2 = 0) and an artificial task can be well-aligned (QR2 = 2).

---

### QR3 — Outcome Measurement

**Question:** Are outcomes measured with validated instruments appropriate to the paper's evaluation goals?

This dimension assesses the validity and appropriateness of outcome measures, not their ecological level (which is captured by EV_Outcome). A validated trust scale (e.g., Trust in Automation — TiA, or Jian et al. Checklist) used in a study explicitly evaluating trust is a QR3 = 2. An unvalidated Likert scale labelled "trust" in a study claiming to evaluate trust calibration is a QR3 = 0.

| Score | Label | Criteria |
|-------|-------|----------|
| 0 | Inappropriate or unvalidated | Outcomes are measured with instruments that are unvalidated, undefined, or inappropriate for the stated outcome. Examples: custom Likert scale labelled "trust" with no reference, reliability, or validation; decision quality claimed but no gold standard used; accuracy computed against a non-clinical reference (e.g., model agreement, not ground truth). |
| 1 | Partially valid | Outcomes measured with partially validated instruments, or validated instruments applied to a different outcome than intended. Examples: validated tool applied but psychometric properties not confirmed in this study's population; decision quality measured but gold standard is weak (e.g., consensus without formal adjudication); multiple outcomes reported but key outcome is unvalidated. |
| 2 | Valid and appropriate | Primary outcome measured with a validated instrument appropriate to the study's stated goals. Validation reference cited. Gold standard clearly defined if decision quality is the outcome. For purely technical evaluations (proxy metrics), the metric is formally defined with a citation to its definition and interpretation. |

**Relationship to EV_Outcome:** EV_Outcome scores the ecological level of the outcome (0–3: no outcome → self-report → decision quality → patient outcomes). QR3 scores the validity of the measurement instrument regardless of the ecological level. A study scoring EV_Outcome = 1 (self-report) can score QR3 = 2 if the self-report instrument is well-validated and appropriate; a study scoring EV_Outcome = 2 (decision quality) can score QR3 = 0 if the decision quality measure is poorly defined.

---

### QR4 — Explanation Faithfulness

**Question:** Does the paper provide any evidence that the explanation reflects what the model is actually doing?

This dimension has no equivalent in the EV rubric. It addresses a fundamental quality concern in XAI research: plausible explanations that do not faithfully represent model behaviour are dangerous in clinical settings — they may increase clinician confidence without warranting it. Adapted from the QUADAS-2 Reference Standard domain (an XAI explanation is a "test" whose "reference standard" is the model's actual computation).

| Score | Label | Criteria |
|-------|-------|----------|
| 0 | No faithfulness assessment | The explanation is presented and evaluated without any assessment of whether it accurately reflects model behaviour. The XAI output is taken at face value. No fidelity metric, stability test, or ground truth comparison is reported. |
| 1 | Indirect or partial assessment | Indirect or qualitative evidence that the explanation is model-faithful. Examples: authors discuss alignment of highlighted features with known clinical risk factors (face validity, not formal verification); explanation is provided by a method with theoretical faithfulness guarantees (e.g., Shapley values) but no empirical verification on this specific model/data combination; sensitivity analysis but no formal fidelity metric. |
| 2 | Direct quantitative assessment | Formal quantitative assessment that the explanation reflects model behaviour. Examples: fidelity score (accuracy of a surrogate model fitted to the XAI explanation); stability metric (explanation consistency across similar inputs); ablation test confirming that features the model weights highly are reflected in the explanation; ground truth comparison using a synthetic dataset where model behaviour is known. |

**Boundary notes:**
- Attention weights presented without verification → QR4 = 0 (attention ≠ faithfulness by default; see xai_method_taxonomy.md coding note)
- SHAP values applied correctly to a tree model (exact Shapley computation) → QR4 = 1 (theoretical guarantee, not empirical verification in this study)
- LIME local approximation validated with fidelity metric reported → QR4 = 2
- Counterfactual explanation validated by running the counterfactual through the actual model and confirming prediction change → QR4 = 2

---

### QR5 — Reporting Completeness

**Question:** Are the XAI method, underlying model, evaluation dataset, and evaluation procedure described with sufficient detail to assess and replicate the study?

This dimension adapts TRIPOD reporting requirements to XAI evaluation papers and incorporates the RoB 2 concern about selective outcome reporting. Reporting completeness is a prerequisite for using the study in synthesis — incompletely reported studies cannot be fully extracted.

| Score | Label | Criteria |
|-------|-------|----------|
| 0 | Major gaps | One or more mandatory elements are absent or described so vaguely as to be uninterpretable. Mandatory elements: (a) XAI method identity and configuration; (b) underlying model architecture or type; (c) dataset identity (at minimum, n, clinical setting, time period); (d) evaluation procedure (how the study was conducted with participants or how metrics were computed). Absence of any single element → QR5 = 0. |
| 1 | Partial reporting | All mandatory elements are present but one or more are insufficiently detailed for replication. Examples: XAI method named but hyperparameters absent; dataset described but size or source not given; evaluation procedure described in abstract terms without operational specifics; pre-specified analysis plan not mentioned (selective reporting risk). |
| 2 | Complete reporting | All mandatory elements reported with sufficient detail: XAI method with configuration parameters; underlying model type and validation approach; dataset with n, clinical setting, and time period; evaluation procedure operational enough to replicate. Pre-specified analysis plan mentioned or full protocol available. Statistical analysis described including how results are summarised. |

**Boundary notes:**
- "We used SHAP" with no further specification → QR5 ≤ 1
- "We used TreeExplainer SHAP (Lundberg & Lee, 2017) on XGBoost (100 trees, max depth 6) with 10-fold cross-validation; n=4,823 ICU admissions from MIMIC-III (2001–2012)" → QR5 = 2 for the model/data element
- Supplementary material containing the full protocol counts toward QR5 = 2 only if it is available (not behind a paywall or "available on request")

---

## 4. Composite Quality Score

A composite quality score (QS_Total) can be computed at analysis time as:

> **QS_Total = QR_Participant + QR_Task + QR_Outcome + QR_Faithfulness + QR_Reporting**
> Range: 0–10

Do not store QS_Total in the schema — compute from the five columns. The profile (five individual scores) is more informative than the composite for diagnosis of specific methodological weaknesses.

**Interpretation guidance:**

| QS_Total range | Interpretation |
|----------------|----------------|
| 0–3 | Low quality — multiple major methodological gaps; use with caution in synthesis; weight-of-evidence sensitivity analysis recommended |
| 4–6 | Moderate quality — notable limitations in at least two dimensions; contribute to synthesis but flag in narrative |
| 7–9 | High quality — minor limitations only; contribute to synthesis without caveat |
| 10 | Exemplary — rare in this literature; flag as methodological reference point |

---

## 5. Scoring Interaction with Study Design

Some QR dimensions have design-conditional interpretation:

| Study Design | QR1 | QR2 | QR3 | QR4 | QR5 |
|-------------|-----|-----|-----|-----|-----|
| MethodPaper (no human evaluation) | Score 2 if claims scoped to technical properties | Score for coherence between demonstration and stated contribution | Score the metric used for demonstration | High bar — method papers should define faithfulness properties | Full bar applies |
| ProxyMetric only (no participants) | Score 2 if claims scoped appropriately | Score for metric-to-RQ alignment | Score the metric's validity | Full bar applies | Full bar applies |
| TrustQuestionnaire only | Full bar — must have appropriate participants for trust claim | Score for alignment between trust measure and trust claim | Must use validated trust scale | QR4 = 0 unless fidelity is also reported | Full bar applies |
| RCT | Full bar | Full bar — randomisation should ensure comparison condition validity | Full bar — primary outcome must be pre-specified | Full bar | Full bar applies — add CONSORT compliance check |
| DownstreamOutcome | Full bar | Full bar | Full bar — patient outcome must be explicitly defined | Full bar | Full bar applies |

---

## 6. Cross-Reference: QR Dimensions vs EV Dimensions

| QR Dimension | EV Dimension | Relationship | Independence |
|-------------|-------------|-------------|-------------|
| QR1 Participant Appropriateness | EV_Participant | EV_P codes participant type (0–3); QR1 codes match between participant type and paper claims (0–2) | **Independent** — a study can have EV_P=1 (non-clinician) and QR1=2 (claims appropriately scoped) or EV_P=3 and QR1=0 (claims overreach participants) |
| QR2 Task Fidelity | EV_Task | EV_T codes task realism (0–3); QR2 codes task-to-RQ alignment (0–2) | **Independent** — a realistic task can be misaligned; an artificial task can be well-aligned |
| QR3 Outcome Measurement | EV_Outcome | EV_O codes ecological level of outcome (0–3); QR3 codes instrument validity (0–2) | **Independent** — self-report (EV_O=1) can use a validated scale (QR3=2); patient outcomes (EV_O=3) can be undefined (QR3=0) |
| QR4 Explanation Faithfulness | None | No EV equivalent | **New dimension** — absent from all standard tools and the EV rubric |
| QR5 Reporting Completeness | None | No EV equivalent | **New dimension** — absent from EV rubric |

The two dimensions with no EV equivalent (QR4, QR5) represent gaps in existing quality frameworks that are particularly consequential for XAI research: unfaithful explanations are dangerous in clinical contexts, and incomplete reporting prevents replication.

---

## 7. Schema Mapping

Five QR columns and one notes column are added to the extraction schema as part of schema v1.2. Code each dimension independently before looking at others.

| Column | Type | Values | Dimension |
|--------|------|--------|-----------|
| `QR_Participant` | ordinal 0–2 | 0=Inappropriate / 1=PartiallyAppropriate / 2=Appropriate | Participant appropriateness |
| `QR_Task` | ordinal 0–2 | 0=Misaligned / 1=PartiallyAligned / 2=WellAligned | Task fidelity |
| `QR_Outcome` | ordinal 0–2 | 0=InappropriateOrUnvalidated / 1=PartiallyValid / 2=ValidAndAppropriate | Outcome measurement |
| `QR_Faithfulness` | ordinal 0–2 | 0=None / 1=Indirect / 2=Direct | Explanation faithfulness |
| `QR_Reporting` | ordinal 0–2 | 0=MajorGaps / 1=Partial / 2=Complete | Reporting completeness |
| `QR_Notes` | string | Mandatory-field gaps (for QR5=0), faithfulness method used (QR4=2), instrument name/citation (QR3) | Free text |

QS_Total (0–10) is computed at analysis time as the sum of the five ordinal scores. Not stored in the schema.

---

## 8. Coding Instructions

1. **Score each dimension independently** before looking at the others. Total score should be computed last.
2. **Score the study as conducted**, not as the authors characterise it. Authors routinely claim high-quality evaluation without meeting the criteria.
3. **Use QR_Notes** to record: the specific instrument name and citation for QR3; the specific faithfulness metric and reference for QR4; the specific field gap for QR5 = 0.
4. **When a paper reports multiple evaluation studies** (e.g., a user study and a deployment study), code the highest quality version achieved on each dimension and note both in QR_Notes.
5. **If a mandatory element cannot be determined from the full text** after reading the Methods, Results, and all available supplementary material, score as if it is absent.

---

## 9. Piloting Protocol

Before full extraction begins:
1. Two reviewers independently code 3 seed papers on all five QR dimensions alongside the EV rubric dimensions.
2. Calculate Cohen's κ for each QR dimension. Target: κ > 0.70 on all dimensions.
3. Resolve disagreements by discussion; document in `memos/decision_log.md`.
4. Pay particular attention to: QR1 (claims matching) and QR4 (faithfulness) — these are the dimensions most likely to require additional boundary rules after piloting.
5. If κ < 0.70 on QR4 after pilot: add worked examples to Section 3 of this document before proceeding.

Seed paper selection: same 3 papers used for EV rubric piloting (Issue #5). Choosing the same papers allows direct comparison of QR and EV codings and may reveal papers where EV and QR are dissociated — a potential finding in itself.

---

## 10. Version History

| Version | Date | Changes |
|---------|------|---------|
| v1 | 2026-05-26 | Initial rubric. Five dimensions (0–2), standard tools mapping, cross-reference to EV rubric, schema column definitions. Issue #20. |
