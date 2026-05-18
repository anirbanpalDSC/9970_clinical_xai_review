# Research Master Memo — Clinical XAI Systematic Review (9970)

Append a dated entry every working day. Never overwrite previous entries.

---

## 2026-05-17

### Insights
- Project initialized. Folder structure, definitions table, and agent instructions established.
- Repo restructured to semantic layout: docs/, data/, notebooks/, scripts/, references/, memos/, project_management/.
- 17 GitHub issues created across Milestones 1–3. Issues are split into intellectual (concept definition, framework building) and infrastructure (schema, logs, tooling). Milestones 4–7 exist but are intentionally empty — filing extraction/synthesis issues before screening is complete is premature.
- Key realization: foundational XAI theory papers (#2, #5, #6) can and should be read before the systematic search runs. They are background/definitional literature, not primary study evidence. They do not appear in the PRISMA count.
- Order of operations established: concept layer (Layer 1) → infrastructure + rubrics (Layer 2) → search and screening (Layer 3). Critical path: #2 + #7 → #10 → #18.
- Decision log established as the canonical place to capture methodological nuances, defenses, and rationale — distinct from this memo. This memo captures observations; the decision log captures decisions.

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
