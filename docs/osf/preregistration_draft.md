# OSF Pre-Registration Draft — Clinical XAI Systematic Review (9970)

**Title:** Explainability in Clinical AI: A Systematic Review of Evaluation Methodology and Ecological Validity
**Date drafted:** 2026-05-24
**Status:** Draft — for OSF submission before search execution
**Contributors:** Anirban Pal
**OSF project:** [to be added at submission]
**PROSPERO registration:** Pending (Issue #19)

---

## 1. Background and Rationale

Explainable AI (XAI) systems for clinical decision support have proliferated rapidly, accompanied by claims that explanations improve clinician trust, decision quality, and ultimately patient outcomes. However, the methods used to evaluate these claims vary enormously — from computational proxy metrics applied without any human participants, to questionnaire studies with lay participants, to rare deployment-embedded trials with licensed clinicians in active clinical workflows.

This variation is not merely methodological diversity. It reflects a structural gap between what clinical XAI papers claim and what they demonstrate. Key distinctions — between explanation plausibility and trust calibration, between participant validity and outcome validity, between workflow realism and ecological validity — are rarely made explicit in the primary literature, creating heterogeneity that makes cross-study synthesis unreliable without a principled evaluation framework.

This review applies a pre-specified extraction schema and a set of pre-registered hypotheses to characterise this gap systematically across the clinical XAI literature published between 2015 and 2024.

---

## 2. Review Question

**Primary question:** What evaluation methods have been used to assess XAI systems in clinical AI, and to what extent do they achieve ecological validity?

**Secondary questions:**
1. What is the relationship between clinician involvement in XAI design and the ecological validity of the resulting evaluation?
2. What proportion of trust-related claims in clinical XAI papers are supported by evidence of trust calibration (rather than explanation plausibility)?
3. Are XAI method types systematically associated with clinical domain, evaluation design, and workflow realism?

---

## 3. Eligibility Criteria

### Inclusion

- **Population/Context:** Clinical AI systems targeting individual patient-level decisions in any clinical domain.
- **Intervention:** Any XAI method applied to, or integrated with, a clinical AI system.
- **Study types:** Any empirical study reporting an evaluation of the XAI component (human-participant studies, proxy-metric-only studies, and deployment studies are all eligible). Method papers with no systematic clinical evaluation are eligible but will be coded `Study_Design: MethodPaper`.
- **Publication period:** 2015–2024 (inclusive).
- **Language:** English.

### Exclusion

- XAI applied to non-clinical AI systems (administrative, financial, operational) with no individual patient decision in the loop.
- XAI applied to population-level or public health decisions (no individual clinician decision required).
- Papers where no licensed clinician is plausibly in the decision loop (fully automated systems without clinical oversight).
- Review articles, editorials, commentaries, and opinion pieces (no primary empirical data).
- Conference abstracts without full-text proceedings.

**Three-gate inclusion boundary (documented in `docs/protocol/inclusion_boundary.md`):**
1. Clinical domain gate: the AI system must target a clinical domain.
2. Individual decision gate: the AI system must support an individual patient-level decision.
3. Clinician loop gate: a licensed clinician must be plausibly in the decision loop.

---

## 4. Extraction Schema

Full schema documented in `data/extraction/schema_v1.csv` and `data/extraction/schema_README.md`.

Key columns relevant to hypothesis testing:

| Column | Role in synthesis |
|--------|------------------|
| `Clinician_Design` | Predictor in H1 |
| `EV_Participant`, `EV_Task`, `EV_Environment`, `EV_Outcome` | Outcome in H1; dissociation test in H6 |
| `XAI_Scope` | Predictor in H2a, H2b |
| `Realism_Level` | Outcome in H2b; prevalence estimate in H5 |
| `Trust_Claim` | Outcome in H3 |
| `Domain`, `XAI_Method` | Variables in H4 |

---

## 5. Pre-Registered Synthesis Hypotheses

Full specification — rationale, extraction fields, analysis, falsification conditions — is in `memos/synthesis_hypotheses.md`. Summaries below.

### H1 — Clinician Co-Design and Ecological Validity

Papers with `Clinician_Design: Yes` will have a higher mean composite ecological validity score (EV_Participant + EV_Task + EV_Environment + EV_Outcome, range 0–12) than papers with `Clinician_Design: No`.

**Analysis:** Mann-Whitney U test (one-tailed). Secondary: dimension-by-dimension comparison with Bonferroni correction.

### H2a — Local Methods Dominate

Local explanation methods (`XAI_Scope: Local`) will constitute > 50% of included papers.

**Analysis:** One-sample proportion test (one-tailed, H₀: proportion ≤ 0.50).

### H2b — Local Methods and Lower Workflow Realism

Among papers with a single explanation scope, `XAI_Scope: Local` papers will have a lower median `Realism_Level` than `XAI_Scope: Global` papers.

**Analysis:** Mann-Whitney U test (one-tailed).

### H3 — Trust Claims Predominantly Reflect Plausibility

Among papers with `Trust_Claim ≠ None`, > 50% will be coded `Plausibility` or `Both` (plausibility demonstrated, calibration not).

**Analysis:** One-sample proportion test (one-tailed, H₀: proportion ≤ 0.50).

### H4 — Domain-Method Coupling

XAI method type (visual saliency vs feature attribution) will be significantly associated with clinical domain (imaging vs tabular/EHR).

**Analysis:** Fisher's exact test on 2×2 contingency table (imaging vs tabular × visual saliency vs feature attribution). Two-tailed (no directional claim on the overall association).

### H5 — Deployment-Embedded Evaluations Are Rare

Fewer than 10% of included papers will be coded `Realism_Level: 4`.

**Analysis:** One-sample proportion test (one-tailed, H₀: proportion ≥ 0.10). Secondary: time trend analysis comparing proportion at Level 4 in Year ≤ 2020 vs Year > 2020.

### H6 — Participant Validity and Outcome Validity Are Dissociated

Among papers with `EV_Participant ≥ 2` (real clinicians), the modal `EV_Outcome` score will be 1 (self-report), not 2 or 3.

**Analysis:** Frequency distribution of EV_Outcome restricted to EV_Participant ≥ 2 papers. Secondary: Fisher's exact test on (EV_Participant 0–1 vs 2–3) × (EV_Outcome 0–1 vs 2–3) across all papers.

---

## 6. Analysis Plan

### 6.1 Descriptive Analysis

Before testing any hypothesis, report:
- Total included papers (N), with breakdown by year, domain, XAI method, study design
- Frequency distributions of all categorical columns
- Median and IQR for all ordinal columns (Realism_Level, EV dimensions)
- Inter-rater reliability (Cohen's κ) for all categorical/ordinal columns from pilot coding (target κ > 0.70 on all columns before full extraction)

### 6.2 Confirmatory Analyses

Run all six hypotheses as specified above. All tests will be reported regardless of significance. Significance threshold: α = 0.05 (corrected for multiple comparisons within H1 secondary analysis only — Bonferroni correction on the four EV dimension tests).

### 6.3 Exploratory Analyses

Any analyses conducted beyond the six pre-registered hypotheses will be explicitly labelled exploratory in the manuscript and will not be used to support primary conclusions.

---

## 7. Inter-Rater Reliability Protocol

Before full extraction:
1. Two reviewers independently code 5 seed papers on all schema columns.
2. Calculate Cohen's κ for each categorical/ordinal column.
3. Target: κ > 0.70 on all columns before proceeding to full extraction.
4. Discrepancies resolved by discussion; resolution logged in `memos/decision_log.md`.

Seed paper selection: draw from included papers after full-text screening. Choose papers spanning at least three domains and two realism levels.

Full protocol documented in `data/extraction/schema_README.md`.

---

## 8. Deviations Protocol

If any hypothesis cannot be tested as specified (e.g., insufficient cell counts for H4, no papers at EV_Participant ≥ 2 for H6), document the deviation in `memos/decision_log.md` before running the analysis. Report all tests, including underpowered ones. Do not drop a hypothesis post-hoc.

Any deviation from this pre-registered plan will be disclosed in the Methods section of the manuscript.

---

## 9. Timeline

| Milestone | Target |
|-----------|--------|
| Pre-registration filed (OSF) | Before search execution |
| PROSPERO registration submitted (Issue #19) | Before search execution |
| Search executed (Issue #22) | After pre-registration confirmed |
| Title/abstract screening | After search |
| Full-text screening | After title/abstract screening |
| Pilot extraction / IRR (5 seed papers) | After full-text screening |
| Full extraction | After IRR confirmed (κ > 0.70) |
| Analysis | After extraction complete |
| Manuscript | After analysis |

---

## 10. Related Protocol Documents

| Document | Purpose |
|----------|---------|
| `docs/protocol/inclusion_boundary.md` | Three-gate inclusion decision rule (Issue #7) |
| `docs/protocol/xai_method_taxonomy.md` | XAI method controlled vocabulary (Issue #6) |
| `data/coding/workflow_realism_rubric.md` | Workflow realism rubric (Issue #4) |
| `data/coding/eval_type_taxonomy.md` | Evaluation type taxonomy (Issue #8) |
| `data/coding/ecological_validity_rubric.md` | Ecological validity rubric (Issue #5) |
| `data/extraction/schema_v1.csv` | Extraction schema (Issue #10) |
| `memos/synthesis_hypotheses.md` | Full hypothesis specifications (Issue #9) |
| `memos/conceptual_distinctions.md` | Trust calibration vs plausibility (Issue #3) |
| `memos/terminology_instability.md` | XAI terminology conflict log (Issue #2) |
| `memos/tag_vocabulary.md` | Semantic tag controlled vocabulary (Issue #13) |

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| Draft v1 | 2026-05-24 | Initial draft. 6 hypotheses. Pre-registered before search execution. |
