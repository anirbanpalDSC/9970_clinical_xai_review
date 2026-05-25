# Evaluation Type Taxonomy — Clinical XAI

**Issue:** #8
**Status:** Resolved 2026-05-24
**Feeds:** `Eval_Type` column in extraction schema (Issue #10)
**Theoretical grounding:** Doshi-Velez & Kim (2017) — three-category framework (Application-grounded / Human-grounded / Functionally-grounded)
**Cross-referenced:** `data/coding/workflow_realism_rubric.md` (Issue #4); `docs/protocol/xai_method_taxonomy.md` (Issue #6)

---

## Purpose

Clinical XAI papers use heterogeneous evaluation approaches that are not directly comparable without a shared taxonomy. This document defines six evaluation types, their operational criteria, minimum study design requirements, limitations, and mapping to the Doshi-Velez (2017) framework. Papers may use multiple evaluation types — multi-coding is expected and required.

---

## Multi-coding Rule

Papers often include multiple evaluation components (e.g., proxy metrics + clinician trust questionnaire). Code **all types present**. Enter them as a semicolon-delimited list in the `Eval_Type` column:

> `ProxyMetric; TrustQuestionnaire`

Order by ecological validity (lowest to highest) when listing. The highest-validity type drives the study's overall quality assessment, but all types must be recorded.

---

## The Six Evaluation Types

### Type 1 — Proxy Metric Evaluation

**Code:** `ProxyMetric`

**Definition:** Quantitative evaluation of the XAI method using computational metrics, with no human participants. Assesses properties of the explanation itself (faithfulness, compactness, stability) or of the explanation model relative to the original black box (fidelity).

**What counts:**
- Faithfulness metrics (e.g., comprehensiveness, sufficiency scores)
- Fidelity/completeness of an explanation model (how well a surrogate matches the original)
- Explanation stability or consistency across runs (LIME instability tests)
- Compactness / sparsity of explanations (number of features used)
- Area-under-the-perturbation-curve (AOPC), insertion/deletion metrics for saliency maps

**Minimum requirements:**
- At least one quantitative metric reported numerically
- Metric computed without human judgment at any stage

**Limitations:**
- Measures explanation properties, not clinical utility
- High proxy metrics do not guarantee usefulness to clinicians
- Fidelity can be high while faithfulness (internal mechanism accuracy) is low — see `memos/terminology_instability.md` Part 3
- No participant → no evidence of comprehension or decision support effect

**Doshi-Velez mapping:** Functionally-grounded

---

### Type 2 — Forward Simulation

**Code:** `ForwardSim`

**Definition:** A human participant is shown an explanation plus the corresponding input data and asked to predict the model's output. Tests whether the explanation successfully transfers the model's decision behavior to a human.

**What counts:**
- Participants are given: (a) explanation of model behavior + (b) new input instance
- Task: predict what the model will output (class label, risk score, or direction of prediction)
- Accuracy of prediction is compared against chance or a baseline condition (no explanation)

**Minimum requirements:**
- Human participants (clinicians or surrogates)
- Comparison baseline (no explanation, or different explanation type)
- Performance measured as prediction accuracy or similar signal-detection metric

**Limitations:**
- Participants learn to predict the *model*, not to make *better clinical decisions*
- High forward simulation accuracy ≠ better clinical judgment — the model may be wrong
- Does not measure whether the explanation is actionable or trusted
- Task is artificial — no clinician is ever asked to predict a model's output in real practice

**Doshi-Velez mapping:** Human-grounded (Simulation-based subtype)

---

### Type 3 — Backward Simulation (Counterfactual Understanding)

**Code:** `BackwardSim`

**Definition:** A human participant is shown an explanation, the input, and the model's output, then asked to identify what would need to change for the model to produce a different output. Tests counterfactual understanding of the decision boundary.

**What counts:**
- Participants are given: (a) explanation + (b) input + (c) model output
- Task: identify which features, if changed, would alter the prediction (counterfactual reasoning)
- Accuracy or quality of counterfactuals compared across explanation conditions

**Minimum requirements:**
- Human participants
- Ground truth counterfactual available (from the model) for comparison
- Accuracy or completeness of participant responses measured

**Limitations:**
- Evaluates counterfactual comprehension, not clinical utility
- Clinically relevant counterfactuals may be physiologically impossible (see XAI method taxonomy: Counterfactual explanations row)
- No evidence that counterfactual understanding improves actual clinical decisions

**Doshi-Velez mapping:** Human-grounded (Simulation-based subtype)

---

### Type 4 — Trust Questionnaire

**Code:** `TrustQuestionnaire`

**Definition:** Self-report measurement of trust, perceived usefulness, or acceptance of the XAI system using standardised or bespoke scales administered after interaction with the AI explanation.

**What counts:**
- Validated scales: Trust in Automation (TiA), Technology Acceptance Model (TAM), System Usability Scale (SUS)
- Bespoke Likert or VAS scales measuring trust, confidence in AI, perceived helpfulness, or willingness to use
- Administered to clinicians or clinical proxies after reviewing AI explanations

**Minimum requirements:**
- Self-report instrument administered post-interaction
- Scale reliability reported (Cronbach's α or equivalent) OR a validated instrument used

**Limitations:**
- Measures *perceived* trust, not calibrated trust — a participant can report high trust in an unreliable explanation
- Susceptible to social desirability bias (participants may report trust to align with perceived researcher expectations)
- Rudin (2019): trust should be calibrated to fidelity; a participant cannot legitimately trust an explanation that is wrong even 10% of the time — self-report does not measure this
- See `memos/terminology_instability.md` Part 1: Trust calibration is not operationalized in any of the 7 foundational papers; trust questionnaire results conflate calibration with plausibility (see Issue #3)

**Coding flag:** Papers that report trust questionnaire results as their *sole* evidence of XAI utility should be flagged `Trust_Only: Yes` in the Notes column.

**Doshi-Velez mapping:** Human-grounded

---

### Type 5 — Decision Quality Study

**Code:** `DecisionQuality`

**Definition:** Measures the accuracy, appropriateness, or quality of clinical decisions made with versus without XAI. The primary outcome is decision quality, not perceptions of the explanation.

**What counts:**
- Diagnostic accuracy (sensitivity, specificity, AUC) of clinician + AI vs clinician alone
- Treatment decision appropriateness rated by clinical experts against a gold standard
- Identification of correct diagnosis/treatment from multiple options, compared across XAI conditions
- Between-subjects or within-subjects design with at least one XAI condition and one control

**Minimum requirements:**
- Comparison condition: with XAI vs without XAI (or different explanation types)
- Clinical decision outcome measured (not self-reported perception)
- Gold standard or expert panel criterion available

**Limitations:**
- Decision quality in artificial tasks (vignettes, retrospective cases) may not transfer to live workflow
- Gold standard definition can be circular if AI training data defines the standard
- Effect size may reflect ceiling effects if the clinical task is easy without AI
- Clinician participants in lab settings may behave differently from real workflow (Hawthorne effect)

**Participant types and realism interaction:**
- Decision quality study with clinical proxies (students, crowd workers) → Human-grounded (lower ecological validity)
- Decision quality study with practicing clinicians in workflow-representative task → Application-grounded (higher ecological validity)
- Record participant type in `Participant_Type` column

**Doshi-Velez mapping:** Application-grounded OR Human-grounded (depends on participant type; see above)

---

### Type 6 — Downstream Outcome Study

**Code:** `DownstreamOutcome`

**Definition:** Real patient outcomes are measured and attributed to clinical decisions informed by XAI. The highest ecological validity evaluation type. Typically a prospective deployment study or RCT.

**What counts:**
- Patient-level clinical endpoints: mortality, length of stay, readmission rate, diagnostic yield, treatment response
- Process outcomes directly linked to AI-assisted decisions: time to diagnosis, change in management rate, rate of guideline-concordant treatment
- Audit of deployed XAI system comparing outcome rates before and after deployment

**Minimum requirements:**
- Prospective data collection after XAI deployment (or well-controlled before-after design)
- Statistical analysis linking XAI use to patient outcomes (not just association between AI accuracy and outcomes)
- Clinical outcome measure must be independent of the AI's prediction target (to avoid tautological assessment)

**Limitations:**
- Confounding is high — many clinical factors affect patient outcomes; isolating XAI effect is difficult without RCT design
- Long time horizons required for outcomes to manifest
- Attribution problem: XAI may improve clinician awareness but the patient outcome depends on many subsequent decisions
- Extremely rare in the current literature — expect < 5% of included papers

**Coding flag:** When present, flag `Level4_Eval: Yes` in Notes — this is a major quality differentiator.

**Doshi-Velez mapping:** Application-grounded

---

## Summary Mapping to Doshi-Velez (2017)

| Doshi-Velez category | Ecological validity | Types in this taxonomy |
|----------------------|--------------------|-----------------------|
| Functionally-grounded | Lowest | `ProxyMetric` |
| Human-grounded | Moderate | `ForwardSim`, `BackwardSim`, `TrustQuestionnaire`, `DecisionQuality` (proxy/lay participants) |
| Application-grounded | Highest | `DecisionQuality` (clinical participants), `DownstreamOutcome` |

Note: `DecisionQuality` spans Human-grounded and Application-grounded depending on participant type. Record `Participant_Type` in the extraction schema to allow post-hoc reclassification.

---

## Controlled Vocabulary for Extraction Schema

Use these exact codes in the `Eval_Type` column of `data/extraction/schema_v1.csv`:

`ProxyMetric` | `ForwardSim` | `BackwardSim` | `TrustQuestionnaire` | `DecisionQuality` | `DownstreamOutcome`

Multi-code with semicolons, ordered lowest to highest ecological validity:
> Example: `ProxyMetric; TrustQuestionnaire; DecisionQuality`

If a paper includes no evaluation of the XAI component (method paper presenting the XAI system without evaluation), enter `None` and note in the Notes column.

---

## Coding Notes

### Attention weights as evidence
Papers that claim interpretability via attention weights without further evaluation should be coded `ProxyMetric` at best, unless a human evaluation accompanies it. See `docs/protocol/xai_method_taxonomy.md` — Attention weights coding note.

### Trust scales with decision quality
If a paper administers both a trust scale and measures decision accuracy, code both `TrustQuestionnaire` and `DecisionQuality`. Do not collapse them.

### Seed paper coding protocol
During pilot extraction (Issue #10), code 5 seed papers independently with a second reviewer. Calculate Cohen's kappa per evaluation type category. Target κ > 0.70 before full extraction. Log discrepancies with paper title, candidate codes, and resolution in `memos/decision_log.md`.
