# Conceptual Distinctions — Clinical XAI Systematic Review (9970)

This document formalises pairs of concepts that the clinical XAI literature treats as equivalent but this review treats as analytically distinct. Each entry states the distinction, the boundary condition, the coding implication, and a worked example.

---

## Distinction 1 — Trust Calibration ≠ Explanation Plausibility

**Issue:** #3
**Status:** Resolved 2026-05-24
**Feeds:** `Trust_Claim`, `Trust_Only`, `Outcome_Claimed`, `Outcome_Demonstrated` in `data/extraction/schema_v1.csv`
**Cross-referenced:** `memos/terminology_instability.md` Part 3; `data/coding/eval_type_taxonomy.md` (TrustQuestionnaire type)

---

### The Distinction

**Explanation plausibility** is a clinician's subjective assessment that an XAI output looks reasonable, coherent, or consistent with their prior knowledge. A clinician finds an explanation plausible when it cites features they expect the model to use — when the explanation fits their mental model of the decision. The typical evidence is self-report: Likert ratings of explanation quality, perceived usefulness scales, or validated questionnaires such as the Trust in Automation scale or System Usability Scale. Plausibility is about human perception of the explanation, not about whether the explanation accurately represents what the model computed. As Lipton (2018) notes, post-hoc explanations can be optimised to produce "misleading but plausible explanations" that satisfy subjective human demands without being faithful to the underlying model; Rudin (2019) strengthens this: a user cannot trust an explanation if the explanation model is wrong even 10% of the time. Plausibility evidence is necessary but not sufficient for trust calibration.

**Trust calibration** is the condition in which a clinician's confidence in an AI system's outputs is proportional to the AI system's actual reliability. A perfectly calibrated clinician trusts the AI's prediction precisely when that prediction is reliable and withholds trust precisely when it is not. Evidence for trust calibration requires three components: (1) a reliability anchor — a measure of the AI's actual performance on a defined clinical task, such as diagnostic accuracy or sensitivity against ground truth; (2) a trust measure — an empirical indicator of clinician confidence in the AI's output, either self-reported or behavioural; and (3) correspondence — evidence that trust covaries appropriately with reliability, whether across cases, across experimental conditions, or over time. Improving trust scores without a reliability anchor does not demonstrate calibration; it demonstrates that clinicians find the AI or its explanations acceptable. The goal of trust calibration — distinct from trust improvement — is that explanations help clinicians avoid both over-trust (accepting predictions the AI gets wrong) and under-trust (rejecting predictions the AI gets right).

---

### Boundary Condition

A study crosses from plausibility into calibration evidence when all three of the following are present:

1. **Reliability anchor:** The study measures the AI system's actual performance on a defined clinical task against a ground truth (e.g., biopsy result, expert consensus, 30-day outcome). Accuracy, sensitivity/specificity, or AUC on the clinical task qualifies. Explanation faithfulness metrics (AOPC, fidelity scores) do not — they measure the explanation's relationship to the model, not the model's relationship to clinical ground truth.

2. **Trust measure tied to the AI's outputs:** The study measures clinician confidence in, acceptance of, or willingness to act on the AI's predictions — not satisfaction with the explanation in the abstract. A trust questionnaire administered after showing explanations and asking clinicians whether they would use the AI in general qualifies. Asking "how convincing is this explanation?" does not.

3. **Covariation evidence:** The study provides evidence that clinician trust tracks AI reliability — not merely that trust increased after explanation exposure. Acceptable forms: trust is higher in conditions where the AI performs better; trust decreases when error cases are shown with explanations; trust calibration is measured directly (e.g., Brier score on clinician confidence, overconfidence/underconfidence decomposition). Acceptable negative evidence that should trigger a `Trust_Claim: Both` code: the paper claims "appropriate trust" or "trust calibration" but measures only trust improvement without reliability covariation.

---

### Coding Instructions

Apply to columns `Trust_Claim`, `Trust_Only`, `Outcome_Claimed`, `Outcome_Demonstrated`.

#### Trust_Claim codes

| Code | Apply when |
|------|-----------|
| `None` | Paper does not make any trust-related claim — trust is not mentioned as an outcome or goal |
| `Plausibility` | Paper demonstrates or claims that clinicians find the explanation plausible, satisfying, or acceptable. Evidence is self-report (questionnaire, Likert, acceptance rating). No reliability anchor required or present |
| `Calibrated` | Paper provides all three components: reliability anchor + trust measure + covariation evidence. Evidence must go beyond "trust increased" |
| `Both` | Paper claims calibration (uses language like "appropriate trust", "trust calibration", "helped clinicians trust the AI correctly") but evidence consists only of trust improvement without a reliability anchor or covariation measure. This is the most common miscoding in clinical XAI |

**Default toward `Both` over `Calibrated`** when a reliability anchor is present but covariation is not demonstrated — improved trust in a study that also reports diagnostic accuracy does not constitute calibration evidence unless the two are linked empirically.

#### Trust_Only flag

Set `Trust_Only: Yes` when a trust questionnaire is the **sole** evaluation of the XAI component — no decision quality measure, no downstream outcome, no proxy metric of explanation faithfulness. This flags papers that claim XAI benefit with no supporting clinical evidence beyond self-report.

#### Outcome_Claimed vs Outcome_Demonstrated

- `Outcome_Claimed`: Copy or close-paraphrase the claim from abstract, introduction, or conclusion. Preserve the authors' language — do not infer.
- `Outcome_Demonstrated`: Summarise what the data actually show, restricted to formally measured outcomes with a comparison condition and appropriate sample size. If nothing is formally demonstrated, leave blank.

The gap between these two columns is the primary evidence for Limitation and Discussion arguments about the field's outcome claim inflation.

---

### Worked Example

**Paradigmatic `Trust_Claim: Both` paper (illustrative, not a real citation)**

Study design: 24 emergency department physicians complete a vignette study. They read 15 clinical cases (simulated from EHR data) and receive a sepsis risk prediction with or without a SHAP explanation. After each batch, they complete a Trust in Medical AI Questionnaire (5-item Likert, validated). Primary analysis: paired t-test comparing trust scores in the explanation vs no-explanation condition.

- **Outcome_Claimed:** "SHAP explanations significantly improved physician trust in the AI sepsis prediction model (p = 0.003). Explanations facilitated appropriate trust calibration, enabling clinicians to better understand and appropriately rely on AI predictions."
- **Outcome_Demonstrated:** Trust questionnaire score increased from 3.4 to 4.1 (7-point scale) in the explanation condition. No sepsis ground truth reported. No analysis of whether trust tracked model accuracy on individual cases.
- **Trust_Claim:** `Both` — paper claims calibration ("appropriate trust calibration", "appropriately rely") but demonstrates plausibility only (questionnaire improvement, no reliability anchor or covariation evidence).
- **Trust_Only:** `Yes` — the trust questionnaire is the sole evaluation of the XAI component.
- **Why not `Calibrated`:** Trust scores increased overall, but the study does not report whether the AI's sepsis predictions were correct. A clinician who trusts a 70%-accurate model at 4.1/7 may be perfectly calibrated, under-trusting, or over-trusting — the data cannot distinguish these. No covariation between trust and case-level accuracy is measured.
- **Why not `Plausibility`:** The authors explicitly claim calibration. The code `Both` captures the gap between what is claimed and what is demonstrated, which is the analytically important finding.

---

### Literature Basis

This distinction is not explicitly operationalised in any of the seven foundational papers reviewed for Issue #2 — trust calibration appears in Part 4 of `terminology_instability.md` as a term absent from all foundational papers. The distinction is constructed from converging partial evidence across three sources:

- **Lipton (2018):** Concern that plausible explanations can be unfaithful — the foundational warrant for distinguishing perception from accuracy.
- **Rudin (2019):** Trust conditioned on near-perfect fidelity — the most restrictive operationalisation of trust in the foundational set, implying that trust levels must be earned through demonstrated explanation accuracy, not just positive affect.
- **Adadi & Berrada (2018):** Trust as a relational property earned through interpretability and verification — closest to calibration in structure, framing trust as something established through the ability to verify, not just to perceive.

**Sourcing note:** During extraction, flag any included paper that operationalises trust calibration directly — a calibration metric, a reliability-trust covariation analysis, or an explicit distinction between trust improvement and trust calibration. These papers should be logged in the conflict log as anchor candidates for `Trust calibration` (currently blank in Part 1 of the terminology table).

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1 | 2026-05-24 | Initial document. Distinction 1 (Trust calibration ≠ Explanation plausibility). Issue #3. |
