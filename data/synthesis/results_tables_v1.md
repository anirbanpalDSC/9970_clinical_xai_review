# Results Tables — RQ1/RQ2/RQ3 (v1, drawn directly from `schema_v1.csv`)

**Source:** `data/extraction/schema_v1.csv`, all 7 included studies, extracted/confirmed 2026-07-23.
**Status:** Draft — RQ1's "EM decision category" column is an inferred dimension (no such column exists in the schema); everything else is a direct pull from extracted columns. Flag/correct as needed before this goes into the manuscript.

---

## RQ1 — Methods and Justification

*Which post-hoc explanation methods are deployed, and what forms of justification are given for their selection?*

| Study | XAI Method | Method_Justification_Type | EM Decision Category (inferred) |
|---|---|---|---|
| Sulaiman_2025 | RuleExtraction | NotReported | Acuity/Triage (early detection of critical outcomes — mortality/ICU within 12h) |
| Sulaiman_2023 | RuleExtraction | NotReported | Disposition (hospitalization prediction) |
| Arnaud_2023 | LIME | Computational | Disposition (admission prediction from triage notes) |
| Juang_2026 | SHAP | Mixed | Disposition (revisit risk → discharge planning) |
| Xie_2021 | RuleExtraction | Mixed | Acuity/Triage (SERP mortality triage score) |
| Han_2025 | SHAP | Mixed | Acuity/Triage (early risk stratification of sting severity) |
| Tang_2026 | LIME | NotReported | Disposition (risk stratification of serious disposition) |

**Method family distribution:** RuleExtraction = 3, SHAP = 2, LIME = 2. No counterfactual, example-based, or attention-based methods appear in this corpus.

**Justification distribution:** NotReported = 3 (43%), Mixed = 3 (43%), Computational = 1 (14%). **Zero papers gave a Cognitive-only or Workflow-only justification** — when a rationale was given at all, it was either purely computational/theoretical grounding (model-agnosticism, Shapley consistency) or a Mixed computational+workflow/cognitive combination. No paper systematically compared its chosen method against alternatives (e.g., "we chose SHAP over LIME because...").

**EM decision category distribution (inferred):** Disposition = 4, Acuity/Triage = 3, Intake = 0.

*Flag: the EM decision category column is my inference from each paper's stated target variable/title, not an extracted schema field. Confirm or correct before use — in particular, `Sulaiman_2023` and `Juang_2026` sit close to the Acuity/Triage-Disposition boundary since both use triage-time features to predict a disposition-shaped outcome.*

---

## RQ2 — Evaluation Rigor

*How do studies evaluate explanation effectiveness across levels of human involvement, and what does the distribution reveal about rigor?*

### Eval_Type distribution

| Eval_Type | Count | Studies |
|---|---|---|
| ProxyMetric | 5 (71%) | Sulaiman_2025, Sulaiman_2023, Xie_2021, Han_2025, Tang_2026 |
| TrustQuestionnaire | 1 (14%) | Juang_2026 |
| None | 1 (14%) | Arnaud_2023 |
| ForwardSim / BackwardSim / DecisionQuality / DownstreamOutcome | 0 | — |

### DoshiVelez_Category distribution

| Category | Count | Studies |
|---|---|---|
| FunctionallyGrounded | 6 (86%) | Sulaiman_2025, Sulaiman_2023, Arnaud_2023*, Xie_2021, Han_2025, Tang_2026 |
| HumanGrounded | 1 (14%) | Juang_2026 |
| **ApplicationGrounded** | **0 (0%)** | — |

*`Arnaud_2023` lands here via the 2026-07-23 tie-break rule (`Eval_Type=None` + `N_Participants>0`), not a clean zero-participant case — see `schema_README.md`.*

### VilonLongo_Category distribution (orthogonal axis)

| Category | Count | Studies |
|---|---|---|
| Objective | 5 (71%) | Sulaiman_2025, Sulaiman_2023, Xie_2021, Han_2025, Tang_2026 |
| HumanCentred_Qualitative | 2 (29%) | Arnaud_2023, Juang_2026 |
| HumanCentred_Quantitative / HumanCentred_Mixed | 0 | — |

### Realism_Level and Ecological Validity (composite EV = sum of 4 dimensions, range 0–12)

| Study | Realism_Level | EV_Participant | EV_Task | EV_Environment | EV_Outcome | EV composite |
|---|---|---|---|---|---|---|
| Sulaiman_2025 | 1 | 0 | 0 | 0 | 0 | 0 |
| Sulaiman_2023 | 1 | 0 | 0 | 0 | 0 | 0 |
| Arnaud_2023 | 1 | 2 | 1 | 0 | 0 | 3 |
| Juang_2026 | 2 | 3 | 1 | 1 | 1 | 6 |
| Xie_2021 | 1 | 0 | 0 | 0 | 0 | 0 |
| Han_2025 | 1 | 0 | 0 | 0 | 0 | 0 |
| Tang_2026 | 1 | 0 | 0 | 0 | 0 | 0 |

**Headline finding:** 6 of 7 studies (86%) sit at `Realism_Level=1` with an EV composite of 0 — a purely computational evaluation of the explanation, no human ever in the loop. The single exception, `Juang_2026` (`Realism_Level=2`, EV composite 6), still falls short of a genuine decision-quality or workflow evaluation — its "highest realism" component is an unvalidated 2-question survey. **No study in this corpus reaches `Realism_Level>=3` or `DoshiVelez_Category=ApplicationGrounded`.** This is the direct evidentiary basis for the paper's central claim: evaluation practice in this corpus clusters almost entirely at the functionally-grounded/objective end, with essentially no clinician-in-the-loop or deployment-embedded evidence.

---

## RQ3 — Regulatory Readiness

*What evidence would satisfy the four regulatory-relevant-evidence criteria, and where are the gaps?*

| Study | Reg_Comprehension | Reg_TrustCalibration | Reg_UncertaintyTransparency | Reg_WorkflowSafety |
|---|---|---|---|---|
| Sulaiman_2025 | No | No | No | No |
| Sulaiman_2023 | No | No | No | No |
| Arnaud_2023 | No | No | No | No |
| Juang_2026 | No | No | No | No |
| Xie_2021 | No | No | No | No |
| Han_2025 | No | No | No | No |
| Tang_2026 | No | No | No | No |

**Proportion meeting each criterion: 0/7 (0%) across all four.** Not one of the 7 included studies provides evidence that would satisfy any of the four regulatory-relevant-evidence criteria operationalized from FDA AI/ML-SaMD guidance and EU AI Act Article 13.

**Representative gaps, by criterion:**
- **Comprehension:** no study administered a comprehension check or correct-interpretation task to any clinician — the closest cases (`Arnaud_2023`, `Han_2025`, `Juang_2026`) have a clinician *viewing or commenting on* an explanation, never *tested* on whether they understood it correctly.
- **Trust calibration:** every `Trust_Claim` in the corpus is `None` (4 studies) or `Plausibility` (3 studies) — **zero studies reach `Calibrated`**. No study measured whether clinician trust actually tracked model correctness across varying reliability conditions; where trust language exists at all, it is either untested rhetoric (`Sulaiman_2025`/`Han_2025` pattern, corrected during review) or thin, unvalidated survey/commentary evidence (`Arnaud_2023`, `Juang_2026`).
- **Uncertainty transparency:** several papers report confidence intervals or discuss model-confidence caveats in their own Discussion sections (`Xie_2021`'s 95% CIs, `Han_2025`'s "clinicians should default to their professional expertise" caveat) — but in every case this is a research-reporting statistic or a stated limitation, never a feature actually surfaced to an end-user at the point of use.
- **Workflow safety:** cross-checks consistently against `Realism_Level<3` and `EV_Environment<2` for all 7 — no study evaluates the explanation within a realistic clinical workflow; `Juang_2026`'s bespoke research interface is the closest attempt and still falls short.

---

## Cross-cutting note (RQ1↔RQ2↔RQ3)

The two studies with the strongest *technical* quality on the extraction's own `QR_*` dimensions (`Xie_2021`, all five QR=2; and to a lesser extent `Han_2025`) are among the studies with **zero** RQ2/RQ3 evidentiary strength — `Xie_2021` in particular is `FunctionallyGrounded`/`Objective`/all-`Reg_*=No` despite being the single best-reported, largest, most rigorously validated paper in the corpus. This is worth stating explicitly in the Discussion: rigorous model-validation methodology and rigorous *interpretability*-validation methodology are not the same thing, and this corpus shows they don't currently travel together.
