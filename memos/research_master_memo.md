# Research Master Memo — Clinical XAI Systematic Review (9970)

Append a dated entry every working day. Never overwrite previous entries.

---

## 2026-05-24

### Issues Resolved
- **Issue #3 (Trust Calibration vs Explanation Plausibility)** — Created `memos/conceptual_distinctions.md`. Formal two-paragraph distinction: plausibility = subjective clinician perception of explanation quality (self-report, no reliability anchor required); calibration = clinician confidence proportional to AI reliability (requires reliability anchor + trust measure + covariation evidence). Boundary: all three components must be present for `Trust_Claim: Calibrated`; presence of reliability anchor alone without covariation defaults to `Both`. Worked example constructed for `Trust_Claim: Both` pattern (most common miscoding). Seed paper coding deferred to pilot extraction. Literature basis: Lipton (plausibility ≠ faithfulness), Rudin (near-perfect fidelity as trust condition), Adadi (trust as relational verification). Trust calibration remains blank in Part 1 of terminology table pending an included paper that operationalises it directly.
- **Issue #4 (Workflow Realism Rubric)** — Committed `data/coding/workflow_realism_rubric.md`. 4-level ordinal scale: Synthetic (1) → Simulated (2) → Ecologically Representative (3) → Deployment-Embedded (4). Each level has operational definition, necessary conditions, positive examples, and boundary decision rules. Critical boundary: real clinical data alone does not elevate the level — the task *structure* and workflow context determine the code. Seed paper coding (IRR target κ > 0.70) deferred to pilot extraction phase (Issue #10).
- **Issue #8 (Evaluation Type Taxonomy)** — Committed `data/coding/eval_type_taxonomy.md`. 6 types: `ProxyMetric`, `ForwardSim`, `BackwardSim`, `TrustQuestionnaire`, `DecisionQuality`, `DownstreamOutcome`. Multi-coding is required; papers commonly combine proxy metrics with questionnaires or decision quality studies. Mapped to Doshi-Velez (2017) 3-category framework. Key flag: `DecisionQuality` can be Human-grounded or Application-grounded depending on participant type — `Participant_Type` field in schema resolves this. `TrustQuestionnaire`-only papers flagged with `Trust_Only: Yes` per Issue #3 concern.

### Design Decisions Made Today
- **Forward vs backward simulation:** Issue #8 distinguishes these as separate types. Forward = predict model output from explanation; Backward = identify counterfactual from explanation. They test different cognitive tasks and should not be collapsed into a single "simulation" code.
- **DecisionQuality spans two Doshi-Velez categories:** Rather than forcing a mapping, `Participant_Type` column in the schema makes the distinction post-hoc. This avoids losing data at extraction time.
- **Level 3 vs Level 4 boundary in realism rubric:** Live deployment alone is not sufficient for Level 4 — the study must also measure real clinical outcomes (diagnostic accuracy on real patients, treatment changes, downstream outcomes). A live deployment study with trust questionnaire only codes as Level 3.
- **Rubric boundary between Level 1 and Level 2:** Real clinical data (MIMIC, DICOM, EHR) used for proxy metric evaluation only (no human, no workflow context) is Level 1, not Level 2. Real data ≠ clinical workflow context.

### Pending (next: Issue #5)
- **Issue #5 (Ecological Validity)** — Four-dimension operationalization (Participant / Task / Environment / Outcome validity). Must cross-reference with the realism rubric — the realism rubric is a holistic ordinal scale; ecological validity is a multi-dimensional profile.

---

## 2026-05-23

### Papers Assessed
- **Miller (2019)** — No new Part 1 definitions. No conflicts logged. Miller is a social science synthesis focused on what makes explanations satisfying to humans (contrastive, selective, social structure) — not an XAI-specific terminology paper. Terms targeted (Justifiability, Trust calibration, Completeness) absent or used only colloquially.
- **Samek et al. (2017)** — No new Part 1 definitions. Corroborates Doshi-Velez (2017) exactly on three terms: Interpretability (same definition, same incompleteness framing), Simulatability (same forward/counterfactual evaluation-task framing), and Trust (same confidence framing, verbatim "aircraft collision avoidance systems" example — direct citation). Two conflict log entries added for Simulatability and Trust confirming Doshi-Velez over Lipton.

### Terminology Status After 6 of 7 Papers
- Blanks remaining in Part 1: Justifiability, Trust calibration, Completeness
- Completeness remains flagged in Part 4 — no technical definition found in any of the 6 papers
- Simulatability conflict (Lipton model-property vs Doshi-Velez/Samek evaluation-task) now 2-vs-1 in favor of Doshi-Velez framing
- Trust conflict (Lipton multi-dimensional vs Doshi-Velez/Samek confidence) now 2-vs-1 in favor of Doshi-Velez framing

### Adadi & Berrada (2018) — Final Paper
- **No new blank terms filled.** Justifiability, Trust calibration, Completeness absent from all 7 papers — confirmed absent and moved to Part 4 with sourcing notes.
- **4 new conflict log entries:** Interpretability (validation framing vs Doshi-Velez communicative framing), Explainability (local/per-prediction vs Arrieta's global/model-level), Trust (third distinct framing: relational outcome between parties — neither Lipton's multi-dimensional nor Doshi-Velez/Samek's confidence), Decomposability (LRP technique vs Lipton's general model property — same technique-as-property conflation pattern seen in the Simulatability conflict).
- **Trust framing tally final:** Lipton (multi-dimensional), Doshi-Velez/Samek (confidence), Adadi (relational). Three distinct framings; none dominant. Lipton retained as anchor for analytical breadth.

### Issue #2 — COMPLETE
All 7 foundational papers assessed. terminology_instability.md is fully populated with all conflicts found. Update GitHub Issue #2 as closed.

---

## 2026-05-17

### Insights
- Project initialized. Folder structure, definitions table, and agent instructions established.
- Repo restructured to semantic layout: docs/, data/, notebooks/, scripts/, references/, memos/, project_management/.
- 17 GitHub issues created across Milestones 1–3. Issues are split into intellectual (concept definition, framework building) and infrastructure (schema, logs, tooling). Milestones 4–7 exist but are intentionally empty — filing extraction/synthesis issues before screening is complete is premature.
- Key realization: foundational XAI theory papers (#2, #5, #6) can and should be read before the systematic search runs. They are background/definitional literature, not primary study evidence. They do not appear in the PRISMA count.
- Order of operations established: concept layer (Layer 1) → infrastructure + rubrics (Layer 2) → search and screening (Layer 3). Critical path: #2 + #7 → #10 → #18.
- Decision log established as the canonical place to capture methodological nuances, defenses, and rationale — distinct from this memo. This memo captures observations; the decision log captures decisions.
- Reference management pipeline established: PDFs in Google Drive → linked in Zotero → BibTeX exported to `references/bib/` in repo. `file = {...}` fields must be stripped before committing; Export Notes must be unchecked. `foundational.bib` committed with 7 papers, years corrected for Lipton (2018) and Samek (2017).
- Samek year discrepancy found and corrected: listed as 2019 in initial decision log entry, actual publication year is 2017. Decision log updated.

### Contradictions
-

### Terminology Conflicts
- Interpretability vs. Explainability distinction must be tracked carefully — literature conflates these heavily. Lipton (2018) is the primary anchor for untangling this.
- Trust vs. trust calibration vs. explanation plausibility: most clinical XAI papers claim trust improvement but measure plausibility only. These are not the same outcome and must be coded separately in the extraction schema (Outcome_Claimed vs. Outcome_Demonstrated).

### Recurring Themes
- Ecological validity is invoked but not operationalized in the XAI literature. This review must define it explicitly across four dimensions: participant, task, environment, outcome validity.
- Workflow realism is a likely axis of heterogeneity — expect most papers to cluster at levels 1–2 (synthetic/simulated), with few at level 4 (deployment-embedded).

### Methodological Weaknesses
- HARKing risk is real in this domain. Pre-registering synthesis hypotheses (#9) before extraction begins is a direct mitigation.
- Relying on self-report trust scales (TiA, Likert) is a known weakness across the clinical XAI literature — flag papers that use only these as ``#explanation_plausibility``.

### Candidate Figures
- PRISMA flow diagram (generated from data/screening/prisma_counts.csv via script)
- XAI method taxonomy table (docs/protocol/xai_method_taxonomy.md)
- Workflow realism distribution across included papers (bar chart)
- Ecological validity score vs. workflow realism scatter

### Synthesis Hypotheses
- Papers reporting clinician involvement in XAI design will show higher ecological validity scores.
- Local explanation methods (SHAP, LIME) will dominate but have lower workflow realism scores than global methods.
- Studies claiming trust improvement will predominantly measure plausibility, not calibration.
- XAI in radiology/pathology will skew toward visual saliency; XAI in EHR prediction toward feature attribution.
- Proportion of deployment-embedded evaluations (realism level 4) will be < 10% of included studies.
