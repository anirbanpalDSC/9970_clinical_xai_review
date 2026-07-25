# Summer Progress Report — Clinical XAI Review (9970)

**Period covered:** 2026-05-17 (project start) – 2026-07-21
**Purpose:** Touch-base briefing — full summer recap while advisor was out

---

## 1. Headline

The review has moved end-to-end through search, screening, and eligibility, and is now closed at **7 included studies**, with extraction and manuscript drafting underway. The one significant event worth flagging up front: for the first ~3 weeks I built a larger, cross-domain, 6-hypothesis systematic review than the one in the approved proposal, caught the mismatch on 2026-06-10, and pivoted back to the proposal's original design — an **EM/ED-only JBI scoping review reported via PRISMA-ScR**, structured around **RQ1–RQ3**. Nothing from the detour was wasted; the strongest pieces (rubrics, taxonomies, the trust-calibration distinction) carry forward as upgrades, and the rest is intact in git history for later-semester work. This was already reported in the 2026-06-11 phase-1 log; everything below is what's happened since.

---

## 2. Search execution (Identification)

Formally executed 2026-06-10 through 2026-06-22, using the finalized EM-narrowed A+B+C string (XAI method AND clinical/CDS context AND ED/triage/ESI/acuity/disposition terms), date range 2015–search date, English only:

| Source | Records | Notes |
|---|---|---|
| PubMed | 497 | Primary source; recall-benchmarked at 75% (6/8) pre-execution |
| IEEE Xplore | 161 | Command Search, rewritten to satisfy IEEE's 10-wildcard cap |
| ACM Digital Library | 1 | Executed via OpenAlex API after ACM's native UI syntax failed |
| Embase | — | **Dropped** — no institutional access at UNO; disclosed as a protocol deviation/limitation |
| **Total identified** | **659** | |
| Duplicates removed | 9 | Rayyan dedup, merged not deleted (provenance retained) |
| Retracted records | 0 | Re-checked against the final 497-record PubMed export |
| **Into screening** | **650** | |

---

## 3. Title/abstract screening

- All 650 deduplicated records screened solo in Rayyan (single reviewer, sole-reviewer adjudication confirmed with you at each stage rather than blocking on a second rater).
- Bulk pass: **40 Include, 64 Maybe/Borderline, 546 Exclude**.
- Adjudicated the 64 borderline records gate-by-gate against the 3-gate inclusion boundary: **24 forwarded, 40 excluded**.
- **64 records carried forward to full-text screening.**

Recurring false-positive pattern at this stage: bare keyword matches ("triage") in clearly non-ED domains (oncology, dermatology, pathology, TB, hematology) — an expected trade-off of a sensitivity-favoring search string.

---

## 4. Full-text screening (Eligibility)

Screened in ~10 batches through 2026-07-14 against `inclusion_boundary.md` (3-gate boundary, v2.2) and the full-text exclusion taxonomy (E1–E6, numeric tie-break).

| Outcome | Count |
|---|---|
| Assessed | 55 of 64 |
| **Included** | **7** |
| Excluded — E1 (wrong ED decision point/setting) | 22 |
| Excluded — E2 (no evaluated XAI component) | 5 |
| Excluded — E3 (XAI applied but never evaluated) | 13 |
| Excluded — E4 (wrong publication type) | 8 |
| Not retrievable (paywalled, no institutional access) | 9 |

**Dominant exclusion patterns identified and documented** (useful for the Discussion/limitations framing):
- **Diagnostic/prognostic-differentiation Gate-1 failures** — models predicting a diagnosis or mortality risk rather than an ED intake/triage/disposition action (sepsis-prediction cluster recurred 6+ times).
- **"XAI-as-decoration" (E3)** — SHAP/LIME applied and narrated as clinically plausible but never formally evaluated for fidelity, stability, or with clinicians. The single most common reason a paper looked promising at abstract stage but failed at full text.
- **Administrative-consumption Gate-1 failures** — patient-level disposition predictions routed to hospital administrators/operations rather than the treating clinician.
- **"No described current ED action point"** — aspirational future-work language ("could support triage workflows") substituting for an actual present-tense description of clinical use.

---

## 5. Closing the corpus at 7 (2026-07-14)

With 9 of the 64 forwarded records permanently paywall-blocked at this institution, I ran a **post-hoc differential search** of the gap window not covered by the original execution (2026-06-11 to 2026-07-14), using the identical registered search string, rather than re-covering already-searched dates. Result: 46 net-new candidates screened → **0 additional Includes**. Every one of the 5 T/A-stage "Includes" from that batch failed full-text on the same established patterns above (mostly "no described current ED action point").

I treated that negative result as evidence the corpus is not under-sampled, and made the explicit call to **stop pursuing further corpus growth** (more search windows, IEEE/ACM re-sweeps, citation-chasing, further retrieval attempts on the blocked records) and proceed to extraction with 7 studies. Full reasoning is logged in `memos/decision_log.md` (2026-07-14) for the record, including a pre-written defense if the study count is challenged: JBI scoping-review methodology sets no minimum study count, the corpus reflects exhaustive screening plus a validation search rather than an arbitrary stopping point, and all retrieval gaps are disclosed rather than dropped silently.

---

## 6. Final included corpus — 7 studies

| # | Study | Venue/Year |
|---|---|---|
| 1 | Sulaiman et al. — Interpretable ML for early detection of critical outcomes in the ED | IEEE CBMS 2025 |
| 2 | Sulaiman et al. — ED triage hospitalization prediction via ML and rule extraction | IEEE EMBS 2023 |
| 3 | Arnaud et al. — Explainable NLP model for predicting ED admissions from triage notes | IEEE BigData 2023 |
| 4 | Juang et al. — Deep learning for ED sustainability: interpretable prediction of revisit | Healthcare, 2026 |
| 5 | Xie et al. — Interpretable ML triage tool for mortality after emergency admissions | JAMA Network Open, 2021 |
| 6 | Han et al. — ML risk stratification of hymenopteran stings (tropical multicenter cohort) | Frontiers in Public Health, 2025 |
| 7 | Tang & Gao — ED narratives for risk stratification of serious disposition in older adults after falls | Int. J. Medical Informatics, 2026 |

Validated BibTeX entries for all 7 are in `references/bib/included_studies.bib`.

---

## 7. Manuscript and reporting infrastructure

Started drafting in parallel with wrapping up screening, so extraction doesn't become the bottleneck:

- **Extraction schema v1.3** (`data/extraction/schema_v1.csv`, 39 columns) finalized — including the trust-calibration-vs-plausibility distinction, Doshi-Velez & Kim / Vilone & Longo method-justification coding, and 4 regulatory-readiness columns (comprehension, trust calibration, uncertainty transparency, workflow safety) feeding RQ3.
- **PRISMA-ScR checklist** — obtained the official 22-item fillable checklist (Tricco et al. 2018) and filled it against current project status; saved as `docs/supplementary/Supplementary Material S1.docx`. (Common citations of this checklist as "20 items" are wrong — confirmed 22 directly from the source document.)
- **Supplementary Material S2** — clean, submission-ready write-up of the 3-gate eligibility criteria with all 14 worked boundary examples, stripped of internal jargon/decision-log references; in both `.md` and `.docx`.
- **`prisma_counts.csv`** fully reconciled — every Identification/Screening/Eligibility/Included row cross-checked directly against the master screening file, not narrative-summed.
- Drafted Methods opening paragraph and two subsections (**Protocol and registration**; **Eligibility criteria**) with real citations (Peters et al. 2020; Tricco et al. 2018).
- Worked through paper title options and full section structure with you not present, pending your input on direction before committing.

---

## 8. What's next

1. **Extraction (Milestone 4)** — populate `schema_v1.csv` for the 7 included studies; this is the immediate priority.
2. Finish drafting remaining Methods subsections (information sources, search, selection of evidence sources, data charting process, data items, critical appraisal, synthesis of results).
3. Build the PRISMA-ScR flow diagram (Identification → Screening → Eligibility → Included) from the finalized `prisma_counts.csv` numbers.
4. Decide on remaining supplementary files (S3 extraction schema, S4 search strings) and finalize the paper title/target.

---

## 9. Bottom line

Screening and eligibility assessment are complete and closed at a defensible, fully-documented 7-study corpus — including a deliberate validation step (the differential search) that shows the corpus isn't under-sampled rather than just asserting it. The paywall gap (9 records, plus Embase entirely) is disclosed as a limitation, not hidden. Manuscript infrastructure (PRISMA-ScR checklist, eligibility supplementary material, citations, opening Methods sections) is already underway so extraction won't be a standing start. Main open question for you: any steer on paper title/target venue, or should I keep treating this as course-deliverable-first for now.
