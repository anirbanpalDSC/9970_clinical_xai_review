# PROSPERO Registration Draft — Clinical XAI Systematic Review (9970)

**Issue:** #19
**Status:** Draft — ready for portal entry
**Portal:** https://www.crd.york.ac.uk/prospero/
**Registration number:** Pending (record after portal submission)
**OSF pre-registration:** https://osf.io/e3ymp/files/3f4am (filed 2026-05-24)

Copy each section below directly into the corresponding PROSPERO form field.
Fields are ordered to match the PROSPERO submission form sequence.

---

## PROSPERO Form Fields

---

### 1. Review title

Explainability in Clinical AI: A Systematic Review of Evaluation Methodology and Ecological Validity

---

### 2. Original language title

Not applicable (review conducted in English).

---

### 3. Anticipated or actual start date of the review

24/05/2026

---

### 4. Anticipated completion date

31/12/2026

---

### 5. Stage of the review at time of this submission

We are registering at the stage of: protocol finalised, search not yet executed.

The following stages are complete:
- Review question defined
- Eligibility criteria specified
- Search strategy drafted (databases identified; search strings in development)
- Data extraction schema finalised (schema v1.2, 33 columns)
- Risk of bias approach defined
- Synthesis hypotheses pre-registered (OSF, 2026-05-24)

The following stages are not yet started:
- Database searches
- Title/abstract screening
- Full-text screening
- Data extraction
- Risk of bias assessment
- Synthesis

---

### 6. Named contact

Anirban Pal

---

### 7. Named contact email

anirbanpal.wbut@gmail.com

---

### 8. Named contact address

Not applicable (independent researcher).

---

### 9. Named contact phone number

Not applicable.

---

### 10. Organizational affiliation of the review

Independent research.

---

### 11. Review team members and their organizational affiliations

Anirban Pal (independent researcher) — review design, search, screening, extraction, synthesis.

---

### 12. Funding sources / sponsors

None declared. This review receives no external funding.

---

### 13. Conflicts of interest

None declared.

---

### 14. Collaborators

None.

---

### 15. Review question

What evaluation methods have been used to assess explainable AI (XAI) systems in clinical decision support, and to what extent do these evaluations achieve ecological validity?

Secondary questions:
1. What is the relationship between clinician involvement in XAI system design and the ecological validity of the resulting evaluation?
2. What proportion of trust-related claims in clinical XAI papers are supported by evidence of trust calibration rather than explanation plausibility alone?
3. Are XAI method types (visual saliency vs feature attribution) systematically associated with clinical domain (imaging vs tabular/EHR)?
4. What proportion of included studies achieve deployment-embedded evaluation (real clinical workflow, real patient outcomes)?
5. Among studies that recruit licensed clinicians as participants, do most measure decision quality or self-reported trust as the primary outcome?

---

### 16. Searches

The following databases will be searched. Search strings are in development and will be finalised before search execution; the search strategy will be documented in full in the review protocol (available at the OSF pre-registration link above).

**Databases:**
- MEDLINE via PubMed
- Embase
- CINAHL (Cumulative Index to Nursing and Allied Health Literature)
- IEEE Xplore
- ACM Digital Library

**Date range:** January 2015 to December 2024 (inclusive). The 2015 lower boundary was selected because foundational XAI methods with clinical applicability (SHAP, LIME, GradCAM) emerged from 2016 onward; a 2015 start date captures the early adoption period without imposing an arbitrary exclusion of potential pre-cursor work.

**Language restriction:** English only.

**Grey literature:** Hand searching of reference lists of included full texts and of key review papers in the domain. No grey literature database searching (PROSPERO protocol registrations, conference abstracts without full proceedings) — these will be excluded at screening per the full-text screening criteria.

**Supplementary search:** Citation tracking of the seven foundational XAI theory papers used to ground operational definitions in this review (Lipton 2018, Doshi-Velez 2017, Adadi 2018, Rudin 2019, Arrieta 2020, Miller 2019, Samek 2017). These foundational papers are background/definitional literature and do not appear in the PRISMA count.

---

### 17. URL to search strategy

Protocol available at: https://osf.io/e3ymp/files/3f4am

Detailed search strings will be appended to the OSF record before execution.

---

### 18. Condition or domain being studied

Explainable AI (XAI) systems applied to clinical decision support across all clinical domains including but not limited to: radiology, pathology, emergency/intensive care, general electronic health records (EHR), cardiology, oncology, and pharmacy.

---

### 19. Population

Clinical AI systems that target individual patient-level decisions in any clinical domain, where a licensed clinician (physician, nurse, radiologist, pathologist, pharmacist, or equivalent) is involved at any stage of the decision pathway (review, validation, action on, or override of AI output).

Population is defined by the three-gate inclusion boundary:
- Gate 1: AI system operates in a clinical or medical domain (diagnosis, prognosis, treatment recommendation, risk stratification, monitoring, imaging, pathology)
- Gate 2: AI output informs a decision about an individual patient's care
- Gate 3: A licensed clinician is in the decision loop at any stage (synchronous or asynchronous)

---

### 20. Intervention(s), exposure(s)

Any XAI method applied to or integrated with a clinical AI system. XAI methods of interest include but are not limited to: SHAP (SHapley Additive exPlanations), LIME (Local Interpretable Model-Agnostic Explanations), GradCAM and variants, attention-based explanations, ANCHOR, counterfactual explanations, prototype-based explanations, and rule extraction methods. Inherently interpretable models (logistic regression, decision trees) are eligible if the paper explicitly evaluates the model's interpretability as an XAI contribution.

---

### 21. Comparator(s) / control(s)

No comparator required for inclusion. This is a methodological review of evaluation practices, not an effectiveness review of XAI clinical outcomes. Where studies include a comparison condition (XAI vs no XAI; XAI method A vs method B), the comparison design will be extracted and characterised.

---

### 22. Types of study to be included

Any primary empirical study reporting an evaluation of an XAI component applied to a clinical AI system, including:
- Randomised controlled trials
- Observational studies (cohort, case-control, cross-sectional)
- User studies with human participants (vignette studies, think-aloud protocols, simulation tasks)
- Proxy-metric-only evaluations (computational evaluation of XAI properties without human participants)
- Deployment studies
- Method papers presenting a new XAI method with a clinical demonstration

Excluded: review articles, editorials, opinion pieces, protocol-only papers, book chapters, and conference abstracts without full proceedings.

---

### 23. Context

Clinical decision support contexts across all clinical specialties and healthcare settings (inpatient, outpatient, emergency, intensive care, imaging, pathology, pharmacy). No geographic restriction.

---

### 24. Primary outcome(s)

This review does not have a single primary outcome in the traditional sense. It is a methodological characterisation review with six pre-registered synthesis hypotheses, each addressing a different dimension of the clinical XAI evaluation literature:

H1: Papers with clinician involvement in XAI design will have a higher composite ecological validity score (EV_Participant + EV_Task + EV_Environment + EV_Outcome, range 0-12) than papers with no clinician design involvement (Mann-Whitney U, one-tailed).

H2a: Local explanation methods will constitute more than 50% of included papers (one-sample proportion test).

H2b: Local explanation papers will have lower median workflow realism scores than global explanation papers (Mann-Whitney U, one-tailed).

H3: More than 50% of papers making trust-related claims will be coded as demonstrating explanation plausibility rather than trust calibration (one-sample proportion test, one-tailed).

H4: XAI method type (visual saliency vs feature attribution) will be significantly associated with clinical domain (imaging vs tabular/EHR) (Fisher's exact test).

H5: Fewer than 10% of included papers will achieve deployment-embedded evaluation status (one-sample proportion test, one-tailed).

H6: Among papers that recruit licensed clinicians as participants (EV_Participant >= 2), the modal primary outcome measure will be self-reported trust (EV_Outcome = 1), not decision quality or patient outcomes (modal frequency test).

Full hypothesis specifications, including rationale, extraction fields, analysis plan, and falsification conditions, are available in the OSF pre-registration record.

---

### 25. Secondary outcome(s)

Descriptive characterisation of the included literature across the following dimensions:
- Distribution of XAI methods across clinical domains
- Distribution of workflow realism levels (ordinal scale 0-4)
- Distribution of ecological validity profiles (four-dimensional: participant, task, environment, outcome validity, each 0-3)
- Distribution of quality scores (five-dimension rubric: participant appropriateness, task fidelity, outcome measurement, explanation faithfulness, reporting completeness, each 0-2)
- Distribution of study designs and evaluation types
- Time trends in realism level and quality scores across the publication window (2015-2024)

---

### 26. Data extraction (selection and coding)

Data will be extracted using a structured 33-column extraction schema (schema v1.2) documented in the review protocol. Key extraction domains:

- Identity (PaperID, Title, Year, Zotero key)
- Clinical domain (controlled vocabulary: Radiology, EHR, Pathology, ICU, Pharmacy, Oncology, Cardiology, Other)
- XAI method (controlled vocabulary: SHAP, LIME, GradCAM, Attention, ANCHOR, Counterfactual, Prototype, RuleExtraction, Other, Multiple) and scope (Local, Global, Both)
- Study design (RCT, Observational, UserStudy, Simulation, MethodPaper)
- Participants (number, type: None/LayPerson/ClinicalTrainee/Clinician/MixedClinical)
- Evaluation type (multi-code: ProxyMetric, ForwardSim, BackwardSim, TrustQuestionnaire, DecisionQuality, DownstreamOutcome, None)
- Workflow realism (ordinal 0-4)
- Ecological validity (four dimensions, each ordinal 0-3)
- Clinician involvement (in evaluation: Yes/No; in design: Yes/No; role)
- Outcomes (claimed vs demonstrated; trust claim type)
- Quality rubric (five dimensions, each ordinal 0-2)
- Semantic tags (controlled vocabulary of 21 tags)

Two reviewers will extract independently for the first 5 papers (pilot). Full extraction will proceed after inter-rater reliability of Cohen's kappa > 0.70 is confirmed on all categorical and ordinal columns. Discrepancies will be resolved by discussion and logged.

---

### 27. Risk of bias (quality) assessment

A custom five-dimension quality rubric was developed and adapted from existing tools because no validated quality assessment instrument exists for XAI evaluation studies, which span proxy-metric, user study, simulation, and deployment designs that do not fit the RCT or diagnostic accuracy study designs assumed by QUADAS-2 or RoB 2.

The five dimensions (each scored 0-2):
1. Participant Appropriateness: match between participant type and the paper's stated claims (adapted from QUADAS-2 Patient Selection)
2. Task Fidelity: alignment between evaluation task design and stated research question
3. Outcome Measurement: validity and appropriateness of measurement instruments (adapted from RoB 2 D4)
4. Explanation Faithfulness: evidence that the explanation reflects actual model behaviour (adapted from QUADAS-2 Reference Standard concept; absent from all standard tools)
5. Reporting Completeness: XAI method, underlying model, dataset, and evaluation procedure described with sufficient detail for assessment and replication (adapted from TRIPOD reporting requirements and RoB 2 D5)

Composite quality score (QS_Total, range 0-10) computed at analysis time. Quality scores will be used in sensitivity analyses (e.g., restricting confirmatory analyses to QS_Total >= 7 papers).

Rationale for custom rubric over standard tools is documented in the review protocol and decision log.

---

### 28. Strategy for data synthesis

Descriptive analysis first: frequency distributions of all categorical variables; median and IQR for all ordinal variables.

Confirmatory analysis: six pre-registered hypotheses tested using pre-specified statistical methods (Mann-Whitney U, one-sample proportion test, Fisher's exact test). Significance threshold alpha = 0.05. All tests reported regardless of significance. Null results are reported as findings.

Bonferroni correction applied only within the secondary dimension-by-dimension analysis for H1 (four EV dimension comparisons). All other tests are reported uncorrected with the pre-registered significance threshold.

Exploratory analyses conducted beyond the six pre-registered hypotheses will be explicitly labelled exploratory in the manuscript and will not be used to support primary conclusions.

Meta-analysis is not planned. Quantitative pooling is not appropriate for a methodological characterisation review of heterogeneous evaluation designs.

---

### 29. Analysis of subgroups or subsets

Pre-specified subgroup analyses:
- H1 secondary: dimension-by-dimension ecological validity comparison (four Mann-Whitney U tests with Bonferroni correction) to identify which EV dimensions drive any composite difference between clinician co-design and non-co-design papers
- H3 secondary: among Trust_Only papers (trust questionnaire as sole evaluation), report proportion and compare workflow realism distribution to non-Trust_Only papers
- H5 secondary: time trend comparison of Realism_Level = 4 papers in Year <= 2020 vs Year > 2020
- H6 secondary: Fisher's exact test on (EV_Participant 0-1 vs 2-3) x (EV_Outcome 0-1 vs 2-3) across all papers

Sensitivity analysis: repeat all confirmatory tests restricted to papers with QS_Total >= 7 (high quality) to assess whether quality moderates the findings.

---

### 30. Type and method of review

Type: Systematic review (methodological / scoping characterisation)
Method: Structured extraction and quantitative summary of study characteristics; no meta-analysis

---

### 31. Language

English.

---

### 32. Country

Not applicable (review covers international literature).

---

### 33. Other registration details

OSF pre-registration filed 2026-05-24 before search execution: https://osf.io/e3ymp/files/3f4am

The OSF record contains: full hypothesis specifications, extraction schema, rubric documents, and the complete review protocol.

---

### 34. Reference and/or URL for published protocol

Protocol available at OSF: https://osf.io/e3ymp/files/3f4am

No journal-published protocol (not planned).

---

### 35. Dissemination plans

Manuscript targeting a peer-reviewed journal in clinical informatics, medical AI, or systematic review methodology. Target journals include: npj Digital Medicine, Journal of the American Medical Informatics Association (JAMIA), Journal of Biomedical Informatics, or PLOS Digital Health.

---

### 36. Keywords

explainable AI; clinical decision support; systematic review; ecological validity; trust calibration; XAI evaluation; machine learning interpretability; clinical AI; human-computer interaction

---

### 37. Details of any existing review of the same topic

A search of PROSPERO conducted on 2026-05-26 identified no registered review with the same focus on evaluation methodology and ecological validity of XAI in clinical AI. Existing reviews in this space focus on XAI methods or clinical domains, not on the validity and quality of the evaluation evidence itself.

---

### 38. Current review status

Ongoing — protocol finalised, search not yet executed.

---

## Submission Checklist

Before submitting to the PROSPERO portal, confirm:

- [ ] Search has not yet run (required — PROSPERO will not accept post-hoc registrations)
- [ ] OSF pre-registration URL confirmed accessible: https://osf.io/e3ymp/files/3f4am
- [ ] All mandatory fields filled (fields 6, 7, 15, 16, 18-28 are mandatory)
- [ ] Anticipated completion date is realistic
- [ ] Registration number recorded in `memos/decision_log.md` after submission confirmation

After registration is published (10-21 days):
- [ ] Record PROSPERO number (format CRD42026xxxxxxx) in `memos/decision_log.md`
- [ ] Add PROSPERO number to `docs/manuscript/` front matter placeholder
- [ ] Add PROSPERO number to `docs/osf/preregistration_draft.md` header

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| Draft v1 | 2026-05-26 | Initial draft. All mandatory PROSPERO fields completed. Ready for portal entry. Issue #19. |
