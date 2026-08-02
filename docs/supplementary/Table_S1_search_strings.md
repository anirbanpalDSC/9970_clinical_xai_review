# Supplementary Table S1: Full Search Strategy by Database

Search strings below are the versions actually executed for this review's primary search (PubMed/MEDLINE, IEEE Xplore, ACM Digital Library). All three share a common three-concept structure: Concept A (explainability/interpretability terms), Concept B (clinical/decision-support context terms), and Concept C (emergency department/triage/acuity/disposition terms), combined with AND. Databases considered but not searched are disclosed at the end of this table rather than omitted silently.

---

## PubMed/MEDLINE

**Executed:** 2026-06-10 **Date range:** 2015/01/01–2026/06/10 **Language:** English **Records retrieved:** 497

```
("explainable artificial intelligence"[tiab] OR "explainable AI"[tiab] OR "XAI"[tiab]
OR "interpretable machine learning"[tiab] OR "interpretability"[tiab] OR "model interpretability"[tiab]
OR "explainability"[tiab] OR "explainable model*"[tiab]
OR "SHAP"[tiab] OR "Shapley additive explanation*"[tiab] OR "Shapley value*"[tiab]
OR "LIME"[tiab] OR "local interpretable model-agnostic"[tiab]
OR "Grad-CAM"[tiab] OR "gradient-weighted class activation"[tiab] OR "class activation map*"[tiab]
OR "counterfactual explanation*"[tiab]
OR "feature attribution"[tiab]
OR "rule extraction"[tiab]
OR "prototype-based explanation"[tiab] OR "prototype explanation*"[tiab] OR "case-based explanation*"[tiab]
OR "interpretable AI"[tiab] OR "interpretable artificial intelligence"[tiab]
OR "explainable deep learning"[tiab])
AND
("clinical decision support"[tiab] OR "clinical decision support system*"[tiab] OR "CDSS"[tiab]
OR "computer-aided diagnos*"[tiab] OR "computer aided diagnos*"[tiab]
OR "diagnostic algorithm*"[tiab] OR "predictive model*"[tiab] OR "risk prediction model*"[tiab]
OR "clinical"[tiab] OR "clinician*"[tiab] OR "physician*"[tiab] OR "radiolog*"[tiab]
OR "patholog*"[tiab] OR "nurse*"[tiab] OR "diagnosis"[tiab] OR "diagnostic"[tiab]
OR "prognosis"[tiab] OR "treatment"[tiab] OR "patient care"[tiab] OR "hospital*"[tiab]
OR "Decision Support Systems, Clinical"[Mesh] OR "Physicians"[Mesh]
OR "Clinical Decision-Making"[Mesh] OR "Diagnosis, Computer-Assisted"[Mesh]
OR "Patient Care"[Mesh])
AND
("emergency department"[tiab] OR "emergency room"[tiab] OR "emergency medicine"[tiab]
OR "emergency severity index"[tiab] OR "ESI"[tiab] OR "Triage"[tiab]
OR "acuity scor*"[tiab] OR "acuity assessment"[tiab] OR "acuity level*"[tiab] OR "acuity classification"[tiab]
OR "disposition decision*"[tiab] OR "ED disposition"[tiab] OR "discharge disposition"[tiab]
OR "patient intake"[tiab] OR "Emergency Service, Hospital"[Mesh] OR "Triage"[Mesh])
AND ("2015/01/01"[Date - Publication] : "2026/06/10"[Date - Publication])
AND English[Language]
```

---

## IEEE Xplore

**Executed:** 2026-06-18 **Date range:** 2015–2026/06/18 **Language:** Not a separate filter field (IEEE Xplore has no language facet; handled at screening) **Records retrieved:** 161

Run via Command Search. Concept terms are translated to IEEE Xplore's field-tag-free syntax; wildcards were reduced from an initial 22 to 6 to satisfy Command Search's 10-wildcard-per-query limit, with the remaining 16 enumerated as explicit word forms instead.

```
("explainable artificial intelligence" OR "explainable AI" OR XAI OR "interpretable machine learning"
OR interpretability OR "model interpretability" OR explainability OR "explainable model" OR "explainable models"
OR SHAP OR "Shapley additive explanation" OR "Shapley additive explanations" OR "Shapley value" OR "Shapley values"
OR LIME OR "local interpretable model-agnostic"
OR "Grad-CAM" OR "gradient-weighted class activation" OR "class activation map" OR "class activation maps" OR "class activation mapping"
OR "counterfactual explanation" OR "counterfactual explanations"
OR "feature attribution" OR "rule extraction"
OR "prototype-based explanation" OR "prototype explanation" OR "prototype explanations"
OR "case-based explanation" OR "case-based explanations"
OR "interpretable AI" OR "interpretable artificial intelligence" OR "explainable deep learning")
AND
("clinical decision support" OR "clinical decision support system" OR "clinical decision support systems" OR CDSS
OR "computer-aided diagnos*" OR "computer aided diagnos*"
OR "diagnostic algorithm" OR "diagnostic algorithms" OR "predictive model" OR "predictive models"
OR "risk prediction model" OR "risk prediction models"
OR clinical OR clinician OR clinicians OR physician OR physicians OR "radiolog*" OR "patholog*" OR "nurse*"
OR diagnosis OR diagnostic OR prognosis OR treatment OR "patient care" OR "hospital*")
AND
("emergency department" OR "emergency room" OR "emergency medicine" OR "emergency severity index" OR ESI OR Triage
OR "acuity score" OR "acuity scores" OR "acuity scoring" OR "acuity assessment" OR "acuity level" OR "acuity levels" OR "acuity classification"
OR "disposition decision" OR "disposition decisions" OR "ED disposition" OR "discharge disposition"
OR "patient intake")
```

---

## ACM Digital Library

**Executed:** 2026-06-22 **Date range:** 2015–2026 **Language:** English **Records retrieved:** 1

ACM Digital Library's Advanced Search bracket-nested field syntax (`[Title: (...)] OR [Abstract: (...)] OR [Keyword: (...)]`) returned 0 results in live testing, including for single-term control queries (e.g., `[Title: "machine learning"]` alone), which ruled out a term/translation problem and pointed to an invalid or UI-only query syntax. ACM Digital Library has no public search API, so the search was instead executed via the **OpenAlex API** (`api.openalex.org`), restricted to ACM as publisher (confirmed publisher ID `P4310319798`), using the same Concept A/B/C term lists as the IEEE Xplore translation above. This is a documented methodology substitution, disclosed the same way as the Embase access gap below, not presented as equivalent to a native ACM Digital Library search.

Query structure (filter parameter):

```
primary_location.source.host_organization:P4310319798,
language:en,
publication_year:2015-2026,
title_and_abstract.search.exact:<Concept A terms, pipe-separated>,
title_and_abstract.search.exact:<Concept B terms, pipe-separated>,
title_and_abstract.search.exact:<Concept C terms, pipe-separated>
```

Result: 1 record (DOI `10.1145/3453166`, "Triage of 2D Mammographic Images Using Multi-view Multi-task Convolutional Neural Networks," 2021). This record is a radiology/mammography image-triage paper, not an ED patient-encounter disposition decision, and is very likely to fail Criterion 1 (Supplementary Material S2) at full-text screening; it is retained in the Identification count rather than pre-filtered, consistent with how every other database's records were handled.

---

## Databases considered but not searched

- **Embase:** Not searched. The reviewer's institution does not subscribe, and no librarian-mediated search was available within the project timeline. Disclosed in the manuscript as a limitation rather than a silently absorbed gap.
- **CINAHL:** Considered during protocol development and shelved when the review's scope was narrowed to emergency-medicine-specific inclusion criteria; not part of the executed search.
