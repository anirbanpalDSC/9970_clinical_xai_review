# Ecological Validity Rubric — Clinical XAI

**Issue:** #5
**Status:** Resolved 2026-05-24
**Feeds:** `EV_Participant`, `EV_Task`, `EV_Environment`, `EV_Outcome` columns in extraction schema (Issue #10)
**Cross-referenced:** `data/coding/workflow_realism_rubric.md` (Issue #4); `data/coding/eval_type_taxonomy.md` (Issue #8)

---

## Purpose and Relationship to the Workflow Realism Rubric

The **workflow realism rubric** (Issue #4) assigns a single holistic score capturing the overall gestalt of how realistic a paper's evaluation is. It answers: *how representative is this study of clinical deployment conditions?*

The **ecological validity rubric** is a four-dimensional profile that answers: *in which specific dimensions does this study achieve validity, and where does it fall short?* A paper can score high on one dimension and low on another — the profile reveals this; the realism rubric does not.

The two rubrics are complementary:
- Realism Level codes go into one column (`Realism_Level`).
- EV dimension scores go into four separate columns (`EV_Participant`, `EV_Task`, `EV_Environment`, `EV_Outcome`).
- A composite EV score is **not** stored in the schema — compute from the four columns at analysis time.
- Typical EV profiles by realism level are given below for consistency checking, but mixed profiles are expected and are themselves a finding.

---

## The Four Dimensions

Each dimension is scored **0–3**. Score the evaluation as conducted, not as authors characterise it.

---

### Dimension 1 — Participant Validity (PV)

**Question:** Are the evaluators actual clinicians operating in their professional practice role and relevant to the AI's target domain?

| Score | Label | Criteria |
|-------|-------|----------|
| 0 | No participants | Evaluation is computational only — no human participants at any stage |
| 1 | Non-clinician | Lay participants, students, crowd workers, or researchers without clinical credentials. Includes medical students and junior trainees where clinical autonomy is not yet established |
| 2 | Clinician, out of role | Licensed clinicians or clinical professionals, but: (a) not in their primary specialty relevant to the AI domain, OR (b) participating outside their clinical workflow (e.g., radiologist in a lab study on cardiology AI) |
| 3 | Clinician, in role | Licensed clinician in the specialty or domain the AI targets, participating in conditions consistent with their actual professional function |

**Boundary notes:**
- A radiologist evaluating chest X-ray AI in a reading session → PV 3
- A radiologist evaluating sepsis prediction AI → PV 2 (wrong specialty)
- A nurse evaluating physician-facing XAI → PV 2 (relevant clinical role but not the decision-maker)
- Mixed clinician/non-clinician participant pool → code the majority group; note in `EV_Notes`

---

### Dimension 2 — Task Validity (TV)

**Question:** Is the decision task representative of real clinical load, time pressure, and information complexity?

| Score | Label | Criteria |
|-------|-------|----------|
| 0 | No task | No human decision task — evaluation is metric-only or XAI output is shown without a decision being elicited |
| 1 | Artificial task | Task is designed by researchers and does not mirror real workflow structure: isolated judgment on a single feature, rating task, preference ranking, or any task that strips away the contextual complexity of real clinical decisions |
| 2 | Simplified representative task | Task mirrors real clinical decision structure (same information format, same decision type) but is simplified: fewer cases than a real session, reduced time pressure, or pre-filtered case set that does not reflect real workload distribution |
| 3 | Fully representative task | Task matches real clinical practice in information load, time available per case, case mix complexity, and decision format — the participant is doing what they would actually do in their clinical role |

**Boundary notes:**
- Likert rating of explanations → TV 1 (rating task, not a clinical decision)
- Vignette study where cardiologist diagnoses 10 cases with/without XAI, no time limit → TV 2
- Radiologist reads AI-assisted worklist of 50 cases under real reading-session time constraints → TV 3
- Forward simulation task (predict model output from explanation) → TV 1 regardless of participant type — this is not a real clinical task

---

### Dimension 3 — Environment Validity (EV_E)

**Question:** Is the XAI tool presented in the actual clinical interface used in practice?

| Score | Label | Criteria |
|-------|-------|----------|
| 0 | No interface | No interface — paper-based scenario, verbal description, or metric computation only |
| 1 | Custom research interface | Purpose-built web app, survey platform, or bespoke prototype not connected to any clinical system |
| 2 | Clinical-like interface | Interface is designed to resemble a clinical system (e.g., mock EHR, simulated PACS viewer) but is not the actual deployed infrastructure |
| 3 | Actual clinical system | XAI is integrated into the real EHR, PACS, LIS, or clinical decision support platform used in the clinical environment being studied |

**Boundary notes:**
- REDCap survey with clinical vignettes → EV_E 1
- Mock EHR (e.g., OpenMRS in a simulation lab) → EV_E 2
- Epic EHR with SHAP sidebar in a deployed pilot → EV_E 3
- Paper printouts of AI output shown to clinicians → EV_E 0

---

### Dimension 4 — Outcome Validity (OV)

**Question:** Are outcomes measured in terms of clinical decisions or patient outcomes, rather than questionnaire responses alone?

| Score | Label | Criteria |
|-------|-------|----------|
| 0 | No outcome / proxy only | No human outcome measured; evaluation consists of proxy metrics computed without participants (faithfulness, fidelity, stability scores) |
| 1 | Self-report only | Primary outcome is participant-reported: trust scale, perceived usefulness, satisfaction rating, or acceptance questionnaire |
| 2 | Decision quality | Primary outcome is the accuracy, appropriateness, or quality of clinical decisions made with versus without XAI, rated against a clinical gold standard or expert panel |
| 3 | Patient outcomes | Primary outcome is a clinical endpoint measured in real patients: mortality, length of stay, diagnostic yield, treatment appropriateness, or a process outcome with direct patient impact |

**Boundary notes:**
- Cohen's kappa on clinician agreement with AI → OV 1 (agreement ≠ decision quality; no gold standard comparison)
- Diagnostic accuracy of clinician+AI vs clinician alone, rated against biopsy/ground truth → OV 2
- 30-day readmission rate after AI-assisted discharge planning → OV 3
- Paper reports both trust questionnaire and decision accuracy → code the highest level (OV 2) and note the questionnaire in `Eval_Type`

---

## Composite Profile and Typical Alignment with Realism Rubric

The EV profile is four scores (PV, TV, EV_E, OV). Do not sum them into a single composite in the schema — the individual profile is more informative.

Typical profiles by realism level (for consistency checking — mixed profiles are expected):

| Realism Level | Typical PV | Typical TV | Typical EV_E | Typical OV |
|---------------|-----------|-----------|-------------|-----------|
| 1 — Synthetic | 0 | 0 | 0–1 | 0 |
| 2 — Simulated | 1–2 | 1 | 1 | 1 |
| 3 — Ecologically representative | 2–3 | 2–3 | 1–2 | 2 |
| 4 — Deployment-embedded | 3 | 3 | 3 | 2–3 |

**Mixed profiles are findings, not coding errors.** A paper at Realism Level 2 with PV=3 (real ICU physicians evaluating vignettes) is worth capturing — it has real participants but an artificial task and interface. The EV profile reveals this distinction; the realism level does not.

**If realism level and EV profile are grossly inconsistent** (e.g., Realism Level 4 but EV_E=1), recheck both codings. Document in `memos/decision_log.md` if the inconsistency is genuine.

---

## Extraction Schema Mapping

| Column | Values | Notes |
|--------|--------|-------|
| `EV_Participant` | 0, 1, 2, 3 | Participant validity score |
| `EV_Task` | 0, 1, 2, 3 | Task validity score |
| `EV_Environment` | 0, 1, 2, 3 | Environment validity score |
| `EV_Outcome` | 0, 1, 2, 3 | Outcome validity score |
| `EV_Notes` | Free text | Document mixed participant pools, boundary calls, or inconsistencies with realism level |

---

## Coding Instructions

1. **Score each dimension independently** before looking at the others. Do not let one high score inflate the others.
2. **Score the evaluation as conducted**, not as described. Authors routinely claim ecological validity without meeting the criteria.
3. **When a paper reports multiple studies or evaluation components at different levels** on the same dimension, code the highest level achieved and note in `EV_Notes`.
4. **Seed paper coding protocol:** During pilot extraction (Issue #10), code 3 seed papers independently with a second reviewer. Calculate per-dimension agreement. Target Cohen's κ > 0.70 on each dimension before full extraction. Log discrepancies in `memos/decision_log.md`.
5. **Boundary between PV 2 and PV 3:** The key question is whether the clinician's role in the study matches their professional decision-making role. A cardiologist reviewing cardiology AI predictions in their clinical specialty at PV 3; the same cardiologist rating AI explanations for interest in a survey → PV 2.
