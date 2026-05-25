# Synthesis Hypotheses — Clinical XAI Systematic Review (9970)

**Issue:** #9
**Status:** Resolved 2026-05-24
**Pre-registration:** `docs/osf/preregistration_draft.md`
**Filed before:** data collection (search not yet run)

All hypotheses are stated before any included papers have been extracted. The search, screening, and extraction will be conducted after this document is committed. This ordering is the anti-HARKing guarantee.

---

## Framing

These hypotheses are confirmatory claims about the *state of the clinical XAI evaluation literature*, not about the XAI methods themselves. They are testable using the extraction schema (`data/extraction/schema_v1.csv`) and do not require access to the raw papers at analysis time — the data fields listed under each hypothesis are sufficient to run the specified analysis.

All hypotheses are pre-registered as directional. A two-tailed test will be used where the direction is not specified; a one-tailed test will be used where the direction is explicitly stated and justified below. Significance threshold: α = 0.05. All analyses will be reported regardless of outcome — null results are findings.

---

## H1 — Clinician Co-Design and Ecological Validity

**Hypothesis:** Papers in which a clinician was involved in designing or developing the XAI system (`Clinician_Design: Yes`) will have a higher mean composite ecological validity score (EV_Participant + EV_Task + EV_Environment + EV_Outcome, range 0–12) than papers with no clinician design involvement (`Clinician_Design: No`).

**Direction:** One-tailed (higher EV in co-design papers).

**Rationale:** Clinician involvement in design is expected to push the evaluation toward conditions that clinicians find credible — real decision tasks, realistic interfaces, and clinically meaningful outcomes. Papers where engineers design the system without clinician input are more likely to use artificial tasks and lab interfaces that satisfy technical reviewers but not clinical validators. This hypothesis is the primary synthesis claim motivating the `Clinician_Design` column split from the original `Clinician_Involved` spec.

**Extraction fields:** `Clinician_Design`, `EV_Participant`, `EV_Task`, `EV_Environment`, `EV_Outcome`

**Derived variable:** `EV_Composite = EV_Participant + EV_Task + EV_Environment + EV_Outcome` (computed at analysis time, not stored in schema)

**Analysis:** Mann-Whitney U test comparing EV_Composite distributions between `Clinician_Design: Yes` and `Clinician_Design: No` groups. Report median and IQR for each group. If n ≥ 30 per group, supplement with Cohen's d for effect size. Secondary analysis: dimension-by-dimension comparison (four separate Mann-Whitney U tests with Bonferroni correction) to identify which EV dimensions drive any composite difference.

**Falsification condition:** No significant difference (p ≥ 0.05, one-tailed), or median EV_Composite is lower in the `Clinician_Design: Yes` group.

---

## H2 — Local Methods Dominate but Carry Lower Workflow Realism

**Hypothesis (two parts):**

**H2a:** Local explanation methods (XAI_Scope: Local) will constitute the majority (> 50%) of included papers.

**H2b:** Among papers using a single explanation scope, papers with `XAI_Scope: Local` will have a lower median `Realism_Level` than papers with `XAI_Scope: Global`.

**Direction:** H2a — proportion test (> 50%). H2b — one-tailed (Local < Global).

**Rationale:** SHAP and LIME produce per-prediction explanations and are computationally tractable for demonstration on individual cases — the format of most simulated and method-paper evaluations. Global methods (rule extraction, prototype-based approaches) require integration into a clinical workflow to be meaningful, because global summaries are only useful when a clinician needs to understand the system's general behaviour — a deployment-level concern. This creates a structural coupling between `XAI_Scope: Global` and higher realism.

**Extraction fields:** `XAI_Scope`, `Realism_Level`

**Analysis:**
- H2a: One-sample proportion test; H₀: proportion of `XAI_Scope: Local` ≤ 0.50.
- H2b: Mann-Whitney U test on `Realism_Level` for `XAI_Scope: Local` vs `XAI_Scope: Global` (exclude `Both` papers). Report median Realism_Level per group.

**Falsification condition:** H2a — proportion of Local papers ≤ 50%. H2b — no significant difference or Global papers have lower median Realism_Level.

---

## H3 — Trust Claims Predominantly Reflect Plausibility, Not Calibration

**Hypothesis:** Among papers that make any trust-related claim (`Trust_Claim ≠ None`), the majority (> 50%) will be coded `Trust_Claim: Plausibility` or `Trust_Claim: Both` — i.e., they claim or demonstrate plausibility without meeting the evidential bar for calibration.

**Direction:** One-tailed (proportion of Plausibility + Both > 50%).

**Rationale:** The foundational literature review found no operationalisation of trust calibration in any of the seven foundational XAI papers. Rudin (2019) requires near-perfect fidelity before trust is warranted; Lipton (2018) documents that plausible explanations can be unfaithful. If neither calibration criteria nor fidelity requirements appear in foundational theory, clinical XAI papers citing this literature are unlikely to meet them in practice. The `Trust_Claim: Both` code was created specifically to capture the pattern where calibration is claimed but plausibility is demonstrated — expected to be the modal code.

**Extraction fields:** `Trust_Claim`, `Trust_Only`

**Analysis:** Frequency distribution of `Trust_Claim` values restricted to papers where `Trust_Claim ≠ None`. One-sample proportion test: H₀: proportion of `Plausibility + Both` ≤ 0.50. Secondary analysis: among `Trust_Only: Yes` papers (trust questionnaire is the sole evaluation), report proportion and compare Realism_Level distribution to papers with `Trust_Only: No`.

**Falsification condition:** Proportion of `Plausibility + Both` ≤ 50% among papers making trust claims, indicating that the majority of clinical XAI papers meet the evidential bar for calibration.

---

## H4 — Domain-Method Coupling (Imaging vs EHR)

**Hypothesis:** XAI method type will be significantly associated with clinical domain: visual saliency methods (GradCAM, Attention) will be more prevalent in imaging domains (Radiology, Pathology); feature attribution methods (SHAP, LIME) will be more prevalent in tabular/EHR domains (EHR, ICU, Pharmacy, Cardiology where non-imaging).

**Direction:** No directional claim on the overall association — the hypothesis is about the pattern of association, not its sign.

**Rationale:** Visual saliency methods are designed for convolutional neural networks applied to image data; they are technically inappropriate for tabular EHR data. Feature attribution methods (SHAP, LIME) are model-agnostic and dominate tabular prediction tasks. The coupling is technical rather than deliberate, but it has consequences for ecological validity: saliency maps require a visual interface (imaging workstation), while attribution methods can be delivered in text-based EHR interfaces. This domain-method coupling therefore has implications for the EV_Environment dimension.

**Extraction fields:** `Domain`, `XAI_Method` (grouped by Tags `#visual_saliency` and `#feature_attribution`)

**Derived groupings:**
- Imaging domains: `Radiology`, `Pathology`
- Tabular/non-imaging domains: `EHR`, `ICU`, `Pharmacy`, `Cardiology` (non-imaging), `Oncology` (non-imaging)
- Method groups: visual saliency (`GradCAM`, `Attention`); feature attribution (`SHAP`, `LIME`)

**Analysis:** 2×2 contingency table (imaging vs tabular × visual saliency vs feature attribution) with Fisher's exact test (chi-square if expected cell counts ≥ 5). Exclude `Multiple`, `Other`, `RuleExtraction`, `Prototype`, `Counterfactual`, `ANCHOR` from the primary analysis (insufficient method specificity for the grouping); report separately. Report row percentages and absolute counts.

**Falsification condition:** Fisher's exact test is not significant (p ≥ 0.05), indicating no domain-method association beyond chance.

---

## H5 — Deployment-Embedded Evaluations Are Rare (< 10%)

**Hypothesis:** Fewer than 10% of included papers will be coded at `Realism_Level: 4` (deployment-embedded evaluation — XAI integrated into active clinical infrastructure with real patient outcomes as the primary endpoint).

**Direction:** One-tailed (proportion < 0.10).

**Rationale:** Deployment-embedded evaluation requires regulatory clearance or approval for clinical use, real patient access, and outcome measurement in routine care — barriers that preclude most academic XAI research groups. The XAI field's trajectory over the 2015–2024 publication window this review covers has been dominated by method development and proof-of-concept demonstrations. A < 10% threshold is consistent with analogous findings in clinical AI validation literature (where deployment studies represent a small minority of total publications).

**Extraction fields:** `Realism_Level`

**Analysis:** One-sample proportion test; H₀: proportion of `Realism_Level: 4` ≥ 0.10. Report exact count and proportion. Secondary analysis: time trend — compare proportion of `Realism_Level: 4` papers in Year ≤ 2020 vs Year > 2020 (Mann-Whitney U on Realism_Level by time period, or Fisher's exact on Realism_Level=4 vs <4 by time period).

**Falsification condition:** Proportion of `Realism_Level: 4` papers ≥ 10%.

---

## H6 — Participant Validity and Outcome Validity Are Dissociated

**Hypothesis:** Among papers where `EV_Participant ≥ 2` (licensed clinicians as participants — in or out of role), the modal `EV_Outcome` score will be 1 (self-report only), not 2 (decision quality) or 3 (patient outcomes). That is, even studies that recruit real clinicians will predominantly measure trust questionnaires rather than decision quality.

**Direction:** One-tailed modal claim (EV_Outcome = 1 is the most common outcome in high-participant-validity papers).

**Rationale:** The ecological validity rubric treats participant validity and outcome validity as independent dimensions — a paper can have real clinicians (PV 3) and still measure only a trust questionnaire (OV 1). The dissociation hypothesis predicts that this is not merely possible but prevalent: the field invests in recruiting appropriate participants but then fails to measure the outcomes that would justify that investment. This would indicate a structural gap — the hard part (clinical participants) is achieved while the methodologically important part (clinically meaningful outcomes) is not. This hypothesis directly motivates the four-dimensional EV profile over a composite score: a composite would mask this dissociation.

**Extraction fields:** `EV_Participant`, `EV_Outcome`, `Eval_Type`

**Analysis:** Restrict to papers where `EV_Participant ≥ 2`. Report frequency distribution of `EV_Outcome` scores (0, 1, 2, 3) within this group. Test whether EV_Outcome = 1 is the modal category. Secondary: cross-tabulate `EV_Participant` (scored as 0–1 vs 2–3) × `EV_Outcome` (scored as 0–1 vs 2–3) with Fisher's exact test to test for independence of the two dimensions across all papers.

**Falsification condition:** Modal EV_Outcome in high-participant-validity papers is 2 or 3, indicating that clinician recruitment and outcome quality co-occur more than predicted.

---

## Hypothesis Summary Table

| ID | Short label | Key columns | Analysis | Direction |
|----|-------------|------------|---------|----------|
| H1 | Co-design → EV | `Clinician_Design`, EV columns | Mann-Whitney U | Higher EV in Yes group |
| H2a | Local methods dominate | `XAI_Scope` | Proportion test | > 50% Local |
| H2b | Local → lower realism | `XAI_Scope`, `Realism_Level` | Mann-Whitney U | Local < Global |
| H3 | Trust claims = plausibility | `Trust_Claim` | Proportion test | > 50% Plausibility+Both |
| H4 | Domain-method coupling | `Domain`, `XAI_Method` | Fisher's exact | Association (no direction) |
| H5 | Deployment < 10% | `Realism_Level` | Proportion test | < 10% at Level 4 |
| H6 | PV–OV dissociation | `EV_Participant`, `EV_Outcome` | Modal frequency | OV=1 modal in PV≥2 papers |

---

## Deviations Protocol

If any hypothesis cannot be tested as specified (e.g., insufficient n per cell for H4, or no papers at EV_Participant ≥ 2 for H6), document the deviation in `memos/decision_log.md` before analysis. Report all tests, including those with n too small for inference. Do not drop a hypothesis post-hoc — analyse and report the null result or the underpowered test.

Exploratory analyses conducted during synthesis that were not pre-registered here will be labelled explicitly as exploratory in the manuscript.
