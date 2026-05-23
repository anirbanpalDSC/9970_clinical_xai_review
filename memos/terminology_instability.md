# Terminology Instability Log — Clinical XAI Systematic Review (9970)

This is a living document. Add a row every time a paper uses a term differently from the working definition, or introduces a distinction not captured here. Never delete rows — add conflict entries instead. This document feeds the Limitations and Discussion sections.

---

## Part 1 — Working Definitions Table

> Fill cells as you read. Leave blank if uncertain — blanks mark what to look for in the next paper.
> Anchor paper = the source you are using to justify this definition.

| Term | Working definition for this review | What it excludes | Anchor paper | Last updated |
|------|------------------------------------|-----------------|--------------|--------------|
| Interpretability | The ability to explain or to present in understandable terms to a human. The need for interpretability arises from an incompleteness in problem formalization — when the objective cannot be fully specified or directly optimized, humans must evaluate the model's behavior through explanation. | Technical performance metrics alone — interpretability is required precisely when those metrics are insufficient | Doshi-Velez & Kim (2017) | 2026-05-22 |
| Explainability | An active characteristic of a model — any action or procedure taken by the model to clarify or detail its internal functions. Acts as an interface between humans and a decision-maker that is both an accurate proxy of the model and comprehensible to humans. | Passive model properties — explainability requires deliberate action, not just inherent structure | Arrieta et al. (2020) | 2026-05-22 |
| Transparency | Informally described as the opposite of opacity or "blackbox-ness". It connotes an understanding of the mechanisms by which a model works and is evaluated at three levels: the entire model, individual components, and the learning algorithm. | Does not require that a human can simulate the model — only that the mechanism is understandable in principle | Lipton (2018) | 2026-05-22 |
| Intelligibility | Equated by referenced literature with understandability — meaning humans can grasp how the model works — and specifically aligns with the property of decomposability where model components admit intuitive explanations. | | Lipton (2018) | 2026-05-22 |
| Justifiability | | | | |
| Trust | Not a single concept; can mean: (1) subjective peace of mind with a model, (2) confidence that a model will perform well when training and deployment objectives diverge, or (3) willingness to relinquish control to an automated system. | A unified or measurable construct — Lipton treats it as underspecified | Lipton (2018) | 2026-05-22 |
| Trust calibration | | | | |
| Explanation plausibility | Not formally defined; post-hoc explanations can be optimized to present "misleading but plausible explanations" satisfying subjective human demands without being faithful to the actual underlying model decisions. | Faithfulness to the model — plausibility is about human perception, not model accuracy | Lipton (2018) | 2026-05-22 |
| Fidelity | | | | |
| Faithfulness | | | | |
| Completeness | | | | |
| Simulatability | A strict form of transparency where a person can contemplate the entire model at once — taking input data and parameters to step through every calculation needed to produce a prediction within a reasonable time. | Models too large or complex to mentally simulate | Lipton (2018) | 2026-05-22 |
| Decomposability | A notion of transparency where every individual part of the model — each input feature, parameter, and calculation — admits an intuitive, plain-text explanation. | Models with components that require domain expertise to interpret | Lipton (2018) | 2026-05-22 |
| Algorithmic transparency | Transparency at the level of the learning algorithm itself — applies when the mathematical behavior of the system is understood, such as being able to prove that training will always converge to a unique solution. | Black-box optimization processes whose convergence or behavior cannot be formally characterized | Lipton (2018) | 2026-05-22 |
| Post-hoc explanation | A distinct category of interpretation methods that extract useful information from a trained model without elucidating its precise internal mechanics. Provides descriptive information for practitioners or end-users. | Methods that make the model itself transparent — post-hoc explanation describes behavior, not mechanism | Lipton (2018) | 2026-05-22 |
| Inherently interpretable model | A model that conveys some degree of interpretability by itself, without requiring post-hoc explanation techniques. | Black-box models that require external explanation methods | Arrieta et al. (2020) — uses "transparent model" as equivalent term; see conflict log | 2026-05-22 |

---

## Part 2 — Conflict Log

> Add a row every time a paper uses one of the above terms in a way that conflicts with the working definition, or uses it differently from another paper already in this log.

| Term | Paper | Definition used in that paper | Conflicts with | Nature of conflict | Notes |
|------|-------|-------------------------------|----------------|--------------------|-------|
| Interpretability vs Explainability | (general) | Used interchangeably across most of the literature | Working definitions in Part 1 | Synonymous use obscures distinct epistemic claims | Primary motivation for this document |
| Simulatability | Doshi-Velez & Kim (2017) | A method of human-grounded evaluation — forward simulation (given explanation + input, predict model output) and counterfactual simulation (given explanation + input + output, identify what must change to alter prediction) | Lipton (2018) — simulatability as a property of the model itself (can a human mentally step through every calculation?) | Lipton defines it at the model level (what the model is); Doshi-Velez reframes it at the task level (how you measure human understanding). A paper running a simulation task is not necessarily evaluating a simulatable model | Critical for coding eval_type in extraction — forward simulation tasks ≠ simulatable models |
| Interpretability | Arrieta et al. (2020) | Passive characteristic of a model — the level at which it makes sense to a human observer | Doshi-Velez & Kim (2017) — interpretability as active ability to explain | Arrieta frames it as an inherent model property (passive); Doshi-Velez frames it as a capability (active). Compatible but different emphasis — Doshi-Velez retained as anchor for its operational precision | Arrieta's passive/active distinction is the key contribution: it sets up the interpretability ≠ explainability split |
| Inherently interpretable model | Arrieta et al. (2020) | Uses "transparent model" as the equivalent term | Part 1 entry which uses "inherently interpretable model" | Terminology conflict — same concept, different label across papers | Rudin (2019) uses "interpretable model"; Arrieta uses "transparent model". Monitor which term dominates in clinical XAI literature during extraction |
| Trust | Doshi-Velez & Kim (2017) | Confidence of human users in system reliability — e.g. "aircraft collision avoidance systems" | Lipton (2018) — trust as multi-dimensional and underspecified | Doshi-Velez narrows trust to a single dimension (confidence); Lipton argues this flattens a genuinely complex construct | Lipton retained as anchor because the multi-dimensional view explains heterogeneity in clinical XAI trust claims. Directly supports Issue #3 argument that clinical XAI papers conflate trust calibration with explanation plausibility |

---

## Part 3 — Distinctions to Track

> Pairs or clusters of terms that the literature treats as equivalent but this review treats as distinct. Updated as reading progresses.

| Distinction | Why it matters for this review | Status |
|-------------|-------------------------------|--------|
| Interpretability ≠ Explainability | Different epistemic claims; conflation makes cross-paper comparison incoherent | **Resolved** — Arrieta (2020): interpretability = passive property of a model; explainability = active process taken by a model. Papers that use them interchangeably will be flagged in the conflict log during extraction |
| Trust calibration ≠ Explanation plausibility | Different outcome claims; most papers claim calibration but demonstrate plausibility only | To be resolved via #3 |
| Fidelity ≠ Faithfulness | Used interchangeably but may encode different evaluation targets depending on sub-field | Monitor during extraction |
| User study ≠ Clinician study ≠ Expert evaluation | Participant type determines ecological validity score | Feeds coding rubric in #4 |
| Interpretable model ≠ Post-hoc explanation | Rudin (2019) draws this distinction sharply; most papers ignore it | Monitor during extraction |

---

## Part 4 — Terms to Watch (not yet conflicting, but unstable)

> Terms encountered that have no stable definition in the literature yet. Flag here; do not add to Part 1 until a working definition can be justified.

| Term | Why flagged | First seen in |
|------|-------------|---------------|
| Completeness | Used by Doshi-Velez as motivational framing (incompleteness of problem formalization) not as a technical property of explanations. The technical sense — an explanation that captures 100% of model mechanics — is not defined by Lipton, Doshi-Velez, or Arrieta. Likely anchored in faithfulness/fidelity literature. Do not add to Part 1 until a paper defines it technically. | Doshi-Velez & Kim (2017) |
| Inherently interpretable model | Arrieta uses "transparent model" as equivalent; Rudin (2019) uses "interpretable model". Term itself is unstable across the literature — the concept is consistent but the label varies. Watch during extraction for which term dominates in clinical XAI papers. | Arrieta et al. (2020) |

---

## Notes

The papers that matter most for #2 specifically:

Read these three first — they do the definitional heavy lifting:

* Lipton (2018) — attacks the conflation directly
* Doshi-Velez & Kim (2017) — proposes a formal definition of interpretability
* Arrieta et al. (2020) — maps the full taxonomy

*The other four come after, and will mostly confirm or add nuance.*
