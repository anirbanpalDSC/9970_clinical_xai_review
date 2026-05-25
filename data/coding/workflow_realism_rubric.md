# Workflow Realism Coding Rubric

**Issue:** #4
**Status:** Resolved 2026-05-24
**Feeds:** `Realism_Level` column in extraction schema (Issue #10)
**Cross-referenced:** `data/coding/ecological_validity_rubric.md` (Issue #5)

---

## Purpose

This rubric operationalizes the degree to which a paper's evaluation mirrors the conditions of real clinical deployment. It provides an ordinal code for the `Realism_Level` column in the extraction schema. The core thesis this rubric tests: XAI is frequently evaluated in conditions that cannot transfer to clinical use — and the distribution of realism levels across the literature is itself a finding.

---

## The Four-Level Scale

### Level 1 — Synthetic

**Definition:** The evaluation uses a constructed or benchmark dataset with no clinical workflow context. The decision task is abstract or domain-agnostic. Clinicians are not involved.

**Necessary conditions (all must hold):**
- Data: publicly available ML benchmark, constructed dataset, or heavily preprocessed data stripped of clinical context
- Task: classification or prediction framed as an ML problem, not as a clinical decision
- Participants: no clinician involvement (researchers, crowd workers, or no human at all)

**Positive examples:**
- LIME or SHAP demonstrated on UCI Heart Disease dataset to show method output
- Faithfulness metrics computed on a neural network trained on MIMIC without clinician evaluation
- XAI method paper using chest X-ray dataset to illustrate attribution maps, not to evaluate clinical utility

**Common miscodings:** A paper that uses real clinical data (EHR, MIMIC, DICOM) but tests only proxy metrics with no human participants is still Level 1 if there is no clinical workflow context — real data alone does not elevate the level.

---

### Level 2 — Simulated

**Definition:** The evaluation uses real clinical data but places participants in an artificially constrained decision task that does not replicate the structure of real clinical decisions. Clinicians or clinical proxies may participate.

**Necessary conditions (at least one):**
- Task is artificially structured by researchers (vignette study, think-aloud on static cases, survey with case descriptions)
- Decision context is isolated from the actual clinical environment (lab, online platform)
- Time pressure, cognitive load, and workflow interruptions characteristic of real clinical settings are absent
- Participants may include clinicians, trainees, or non-clinician surrogates (medical students, crowd workers)

**Positive examples:**
- Emergency physicians review 10 static case vignettes with/without SHAP explanations in a survey
- Radiologists label AI-highlighted regions as "correct" or "incorrect" in a web interface outside their PACS
- Nurses rate the usefulness of AI risk scores on Likert scales after reading a written scenario
- Think-aloud study where clinicians narrate while reviewing AI explanations on printed case summaries

**Boundary with Level 1:** Level 2 requires either real clinical data or real clinical participants. A paper with benchmark data and no human participants is Level 1 even if the paper describes a "simulation."

**Boundary with Level 3:** Distinguish whether the task *structure* (not just the data) mirrors real workflow. A vignette with real EHR data is Level 2. A prospective structured decision task that mirrors ICU rounds (same time per case, same information available, same format as actual rounds) is Level 3.

---

### Level 3 — Ecologically Representative

**Definition:** The evaluation uses real clinical data and preserves the structure, sequence, and time constraints of actual clinical decision-making, but is not embedded in an active live workflow.

**Necessary conditions (all must hold):**
- Data: real patient data, not vignettes or artificially constructed cases
- Participants: practicing clinicians in their actual professional role (radiologist, intensivist, pathologist, etc.)
- Task structure: mirrors real clinical workflow — same information availability, same decision format, similar time pressure
- Environment: may be prospective or retrospective but typically not live workflow (e.g., structured reading session with de-identified cases)

**Positive examples:**
- Radiologists review AI-prioritised worklist of de-identified chest X-rays in a structured session mirroring PACS workflow, measuring diagnostic accuracy with/without AI
- ICU physicians review SHAP-augmented mortality risk scores for de-identified ICU patients in a session structured like morning rounds
- Pathologists assess slides with/without AI annotations in a reading session that replicates their actual slide review process

**Boundary with Level 2:** The distinguishing criterion is whether the task structure, not just the data source, mirrors real clinical decision-making. If the task format is designed by researchers to isolate a specific judgment (e.g., "does explanation help you identify the feature driving the prediction?"), it is Level 2 even with real participants and real data.

**Boundary with Level 4:** Level 3 studies are not embedded in live care delivery. No real-time patient care decisions are made; no actual clinical outcomes flow from the study decisions.

---

### Level 4 — Deployment-Embedded

**Definition:** The XAI tool is integrated into the active clinical workflow during the study period, and real clinical outcomes — not just perceptions or preferences — are measured.

**Necessary conditions (all must hold):**
- XAI tool is live in the clinical environment (EHR integration, PACS plugin, clinical decision support alert, etc.)
- Clinicians use the tool during real patient care
- The study measures real clinical outcomes or decision outcomes (e.g., diagnostic accuracy on real cases, treatment changes, downstream patient outcomes), not just questionnaire responses
- Prospective design (retrospective chart review of a deployed system may qualify if outcomes are primary)

**Positive examples:**
- Prospective RCT where emergency physicians receive LIME explanations in live EHR; primary endpoint is rate of missed diagnoses over 6 months
- Before-after deployment study measuring whether sepsis alert explanations change antibiotic administration patterns in ICU
- Radiologist reads AI-assisted mammography in live screening workflow; audit of recall rates before and after deployment

**Note on mixed designs:** A study that deploys XAI in a live setting but measures only trust questionnaire responses should be coded Level 3, not Level 4 — the clinical outcome criterion distinguishes Level 3 from Level 4.

---

## Decision Rules for Boundary Cases

| Scenario | Code | Rationale |
|----------|------|-----------|
| Real clinical data, proxy metrics only, no human participants | 1 | No workflow context, no human element |
| Vignette study with real clinicians, real case descriptions (not real EHR data) | 2 | Artificial task format |
| Online survey with real EHR data excerpts, real clinicians | 2 | Lab/online context, not workflow-embedded |
| Structured reading session with real de-identified cases, practicing radiologists | 3 | Real participants + task structure mirrors real workflow, but not live care |
| Wizard-of-oz pilot deployment where AI explanations are shown to clinicians in a mock version of the live system | 3 | Task structure realistic but not actual live deployment with real patient outcomes |
| Prospective deployment in live EHR, outcomes = trust questionnaire only | 3 | Live deployment but no clinical outcome measure |
| Prospective deployment in live EHR, outcomes = diagnostic accuracy on real patients | 4 | Full deployment + real clinical outcome |
| RCT where AI is the intervention, clinicians treated as users, patient outcomes measured | 4 | Standard Level 4 case |

---

## Coding Instructions

1. **Code the evaluation as actually conducted**, not as the authors describe it. Authors frequently claim ecological validity or clinical relevance without meeting the criteria above.
2. **If a paper reports multiple evaluation components at different levels** (e.g., proxy metrics + clinician vignette), code the highest level achieved and note in the `Realism_Notes` column.
3. **Seed paper coding protocol:** During pilot extraction (Issue #10), code 5 seed papers independently with a second reviewer. Calculate Cohen's kappa. Target κ > 0.70 before full extraction begins. Log discrepancies with paper title and rationale in `memos/decision_log.md`.
4. **Ambiguous cases:** When the realism level is unclear after applying the decision rules, code as the lower level and document in `memos/decision_log.md` with paper title, candidate levels, and reason for uncertainty.

---

## Extraction Schema Mapping

| Rubric level | `Realism_Level` code |
|--------------|---------------------|
| 1 — Synthetic | `1` |
| 2 — Simulated | `2` |
| 3 — Ecologically representative | `3` |
| 4 — Deployment-embedded | `4` |

If the paper does not include any evaluation of the XAI component (method paper only), enter `0` (No evaluation) and document in Notes.
