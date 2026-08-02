# Supplementary Material S2: Eligibility Criteria — Full Operational Definitions

A source of evidence was eligible for inclusion if it passed all three of the following criteria, applied in sequence.

---

## Criterion 1 — Emergency Department Encounter Scope

The predictive model's decision point had to occur during the **initial emergency department (ED) encounter**, corresponding to one of three categories:

(a) **Initial patient intake** — e.g., chief-complaint screening, initial vitals-based risk flagging at ED arrival
(b) **Acuity or triage scoring** — e.g., Emergency Severity Index (ESI) assignment, or an equivalent acuity scale (e.g., CTAS, MTS, ATS)
(c) **Immediate disposition** — admission, discharge, transfer, or ICU-admission decisions made at the point of ED care

These three categories are exhaustive: an ED-encounter decision point that does not fall into one of them (e.g., an in-ED treatment or procedural decision, such as real-time resuscitation management) did not satisfy Criterion 1, even in the absence of any other disqualifying feature.

**Sources were excluded on this criterion if:**
- The decision point occurred before ED arrival (pre-hospital or emergency medical services triage/transport decisions), regardless of whether the patient was subsequently seen in the ED.
- The decision point occurred after ward or ICU admission (inpatient deterioration/monitoring, ICU-specific management, mortality, or prognosis models), regardless of whether the derivation or validation cohort originated in the ED.
- The model addressed an operational or administrative outcome (e.g., ED crowding, throughput, staffing) rather than an individual-patient intake, acuity, or disposition decision.
- The model addressed an in-ED treatment, procedural, or physiologic-monitoring decision (e.g., real-time resuscitation management, medication dosing, imaging acquisition or interpretation for diagnosis) that occurred during the ED encounter but was not itself an intake, acuity/triage, or disposition decision.
- The model produced a patient-level, disposition-shaped prediction (e.g., admit versus discharge) but the paper described that output as being consumed by administrators or operational systems for capacity, staffing, or surge-management purposes, rather than returned to the treating clinician to inform that patient's own care.

**Operational test applied throughout:** the deciding question was *where and when the model's output was acted upon*, not where the underlying data originated. A model derived from an ED-admitted cohort but intended to support a decision made outside the ED (e.g., an inpatient-team decision made after admission) did not satisfy this criterion. Conversely, a model predicting a future event (e.g., 30-day readmission risk computed at ED discharge to inform the discharge decision itself) satisfied this criterion, because the action point — the discharge decision — occurred in the ED, even though the predicted outcome occurred later.

---

## Criterion 2 — Explainable or Interpretable AI Method

The source had to apply, evaluate, or propose one of the following:

- A **post-hoc explanation method** (e.g., feature-attribution methods such as SHAP or LIME; counterfactual explanation; example- or case-based explanation; rule extraction) applied to a predictive model addressing a Criterion-1 decision; **or**
- An **inherently interpretable model** (e.g., logistic regression, decision tree, rule list) for which the source explicitly evaluated or discussed the model's interpretability as a contribution of the work, rather than using an interpretable model incidentally with no discussion of its interpretability.

Sources reporting predictive models for Criterion-1 decisions with no interpretability or explanation component (i.e., pure black-box performance studies) did not satisfy this criterion.

---

## Criterion 3 — Empirical Evaluation of the Explanation Component

The source had to report at least one empirical evaluation of the explanation method itself — not solely of the underlying predictive model's accuracy — corresponding to at least one of the following six levels:

1. Computational or fidelity metrics (proxy-metric evaluation)
2. Forward simulation (participant predicts the model's output from the explanation)
3. Backward simulation (participant reasons about what would change the model's output)
4. Trust questionnaire (self-report of trust, usefulness, or acceptance)
5. Decision-quality study (measured accuracy or appropriateness of decisions made with the explanation)
6. Downstream-outcome or real-world deployment evaluation

Review articles, editorials, commentaries, and opinion pieces with no underlying empirical study, protocol-only publications with no results reported, and conference abstracts without an associated full-length proceedings paper did not satisfy this criterion.

---

## Exclusion Reason Taxonomy

When a source failed to meet the eligibility criteria above, one exclusion reason was assigned from the controlled list below. Where a source could be excluded for more than one reason, the lower-numbered (higher-priority) code was assigned by default, with one exception: a source whose failure of Criteria 1-3 stemmed solely from its being a review, editorial, commentary, protocol-only, or abstract-only publication was coded as a wrong publication type (E4) rather than E1, since applying E1 to every such source would otherwise make E4 unusable for its intended purpose.

| Code | Label | Definition |
|------|-------|------------|
| E1 | Not a clinical AI application | Failed Criterion 1, 2, or 3 above. Includes administrative AI, consumer-facing health AI, drug discovery, population-only analytics, or the absence of a clinician in the decision loop. |
| E2 | No XAI component | A clinical AI system was evaluated, but no explanation method meeting Criterion 2 was applied. Includes model-performance evaluations with no explanation output, and feature importance reported from the model itself without XAI framing. |
| E3 | XAI not evaluated | An explanation method was applied and described but not evaluated in any form meeting Criterion 3: no proxy metric, no human evaluation, and no authorial claim that the explanation component was being evaluated. |
| E4 | Wrong publication type | Review article, systematic review, editorial, opinion piece, commentary, protocol paper without results, book chapter, or conference abstract without full proceedings. Applied even where substantive XAI content was present, and applied in place of E1 when a source's failure of Criteria 1-3 stemmed solely from its being one of these publication types. |
| E5 | Insufficient extraction detail | The source passed Criteria 1-3 but did not report enough methodological detail to complete the mandatory data-extraction fields. |
| E6 | Duplicate report | A different report of a study already included (for example, a conference version of an included journal paper, or the same dataset with a minor extension). Where both reports contributed extractable data not present in the other, both were included and cross-referenced; where one report was a strict subset of the other, only the more complete report was included. |

### E3 versus the method-paper exception

Papers presenting a novel explanation method with a clinical demonstration case, but without a systematic evaluation of clinical utility, were included rather than excluded under E3, provided the explanation method was the paper's stated primary contribution. A post-hoc explanation figure included incidentally within a clinical-prediction paper did not qualify for this exception.

| Description | Decision | Rationale |
|---|---|---|
| "We propose XAI-Net for chest X-ray diagnosis and evaluate its faithfulness and clinician acceptance across three hospitals." | Include | The explanation method is the stated contribution, and the paper evaluates it. |
| "We trained XGBoost for ICU mortality prediction (AUROC 0.84). Figure 3 shows SHAP feature importance." | Exclude (E3) | The explanation is incidental; no evaluation of it is reported. |
| "We use LIME to explain our sepsis prediction model. Clinicians rated explanations on a 5-point scale." | Include | The explanation is evaluated via a human-participant rating. |
| "We present a logistic regression model for readmission risk. Odds ratios are reported in Table 2." | Exclude (E2) | Model coefficients alone do not constitute an explanation method. |

---

## Worked Examples

| Description | Criterion 1 | Criterion 2 | Criterion 3 | Decision | Rationale |
|---|---|---|---|---|---|
| ED sepsis early-warning model with SHAP explanation, used by ED physicians to decide immediate admission versus discharge | Pass | Pass | Pass (clinician-in-the-loop) | Include | Decision point and action both occur in the ED |
| ESI acuity-prediction model with attention-based explanation, evaluated via a nurse usability study on simulated triage vignettes | Pass | Pass | Pass (simulated-user) | Include | Acuity scoring satisfies Criterion 1; a simulated-user study is a valid evaluation level |
| Pre-hospital EMS stroke-triage model with counterfactual explanations, used by paramedics before ED arrival | Fail | — | — | Exclude | Decision point precedes ED arrival |
| Sepsis deterioration model with SHAP for inpatient ward monitoring; derivation cohort drawn from ED-admitted patients | Fail | — | — | Exclude | Decision point is the inpatient ward, not the initial ED encounter; cohort origin does not change this |
| ICU mortality-prediction model with LIME explanations, used for ICU triage following ED-to-ICU admission | Fail | — | — | Exclude | Decision point is the ICU |
| ED-discharge 30-day-readmission risk model with feature-attribution explanation, reviewed by the ED physician at the point of the discharge decision | Pass | Pass | Pass | Include | The action point (the discharge decision) is in the ED even though the predicted outcome occurs later |
| Pediatric febrile-infant ED risk-stratification tool using a rule-based (decision-tree) model, evaluated only via computational fidelity metrics, with no clinician study | Pass | Pass | Pass (computational) | Include | An inherently interpretable model explicitly evaluated for interpretability; a computational fidelity metric is a valid evaluation level |
| Novel counterfactual-explanation method demonstrated on a general intensive care dataset, with no ED-specific framing | Fail | — | — | Exclude | Not an ED-encounter decision |
| Narrative review of explainable AI approaches for ED triage, with no novel model or empirical evaluation | Pass | Pass (discusses methods) | Fail | Exclude | No empirical evaluation of an explanation component; also excluded as a non-empirical review |
| ED crowding/throughput-prediction model with a SHAP explanation, intended for hospital administrators | Fail | — | — | Exclude | Not a patient-level intake, acuity, or disposition decision |
| ESI triage model with example-based explanations, evaluated via a clinician-in-the-loop study conducted in a simulation laboratory rather than live ED workflow | Pass | Pass | Pass | Include | All three criteria are satisfied; the realism of the evaluation setting is captured at the data-extraction stage rather than applied as an eligibility criterion |
| Multi-setting study evaluating the same explainable sepsis model at ED triage, on inpatient wards, and in the ICU | Pass (ED-triage component only) | Pass | Pass | Include (ED-triage component only) | Only the ED-triage decision and its evaluation were extracted; inpatient and ICU components were treated as out of scope. Where results were not reported separately by setting, the source was instead escalated as a borderline case for adjudication rather than included by default. |
| Model predicting shockable cardiac rhythm from electrocardiogram data during active cardiopulmonary resuscitation in the ED, with a class-activation-map explanation | Fail | — | — | Exclude | Although the population and setting are the ED, the decision point is a real-time treatment/procedural decision, not intake, acuity/triage scoring, or disposition |
| Combined machine-learning and large-language-model tool predicting individual-patient ED disposition before physician evaluation, explicitly intended to give hospital administrators early notice for bed allocation and staffing, with a SHAP explanation | Fail | — | — | Exclude | Although the prediction is patient-level and disposition-shaped, the output is consumed administratively rather than by the treating clinician |

---

## Additional Operational Notes

- **Acuity-scale terminology:** the Emergency Severity Index (ESI) is used as the reference example throughout, but other national acuity or triage scales (e.g., CTAS, MTS, ATS) were treated as in scope under the acuity-scoring category.
- **Scope of "immediate disposition":** limited to admission, discharge, transfer, or ICU-admission decisions made at the point of ED care; downstream decisions made by an inpatient team after the disposition decision itself were out of scope.
- **Interpretable-model threshold (Criterion 2):** the use of an inherently interpretable model (e.g., logistic regression) alone was not sufficient to satisfy Criterion 2 — the source had to explicitly frame or evaluate the model's interpretability as relevant to the work.
