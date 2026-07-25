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

The source had to report at least one empirical evaluation of the explanation method itself — not solely of the underlying predictive model's accuracy — corresponding to at least one of the following levels:

1. Computational or fidelity metrics
2. Proxy tasks
3. Simulated-user studies
4. Clinician-in-the-loop studies
5. Real-world deployment evaluation

Review articles, editorials, commentaries, and opinion pieces with no underlying empirical study, protocol-only publications with no results reported, and conference abstracts without an associated full-length proceedings paper did not satisfy this criterion.

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
| Multi-setting study evaluating the same explainable sepsis model at ED triage, on inpatient wards, and in the ICU | Pass (ED-triage component only) | Pass | Pass | Include (ED-triage component only) | Only the ED-triage decision and its evaluation were extracted; inpatient and ICU components were treated as out of scope |
| Model predicting shockable cardiac rhythm from electrocardiogram data during active cardiopulmonary resuscitation in the ED, with a class-activation-map explanation | Fail | — | — | Exclude | Although the population and setting are the ED, the decision point is a real-time treatment/procedural decision, not intake, acuity/triage scoring, or disposition |
| Combined machine-learning and large-language-model tool predicting individual-patient ED disposition before physician evaluation, explicitly intended to give hospital administrators early notice for bed allocation and staffing, with a SHAP explanation | Fail | — | — | Exclude | Although the prediction is patient-level and disposition-shaped, the output is consumed administratively rather than by the treating clinician |

---

## Additional Operational Notes

- **Acuity-scale terminology:** the Emergency Severity Index (ESI) is used as the reference example throughout, but other national acuity or triage scales (e.g., CTAS, MTS, ATS) were treated as in scope under the acuity-scoring category.
- **Scope of "immediate disposition":** limited to admission, discharge, transfer, or ICU-admission decisions made at the point of ED care; downstream decisions made by an inpatient team after the disposition decision itself were out of scope.
- **Interpretable-model threshold (Criterion 2):** the use of an inherently interpretable model (e.g., logistic regression) alone was not sufficient to satisfy Criterion 2 — the source had to explicitly frame or evaluate the model's interpretability as relevant to the work.
