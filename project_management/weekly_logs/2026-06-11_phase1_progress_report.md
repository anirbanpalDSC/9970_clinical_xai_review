# Phase 1 Progress Report — Clinical XAI Review (9970)

**Period covered:** 2026-05-17 (project start) – 2026-06-11
**Maps to proposal:** Phase 1, "Protocol Definition and Literature Discovery" (Weeks 1–3)

---

## 1. Headline

Phase 1 is functionally complete, but I want to be upfront that the route here was not direct. For roughly the first three weeks I built out a substantially **larger and more ambitious review than the one in the approved proposal** — a cross-domain (not EM-only), 6-hypothesis confirmatory systematic review across five databases. On 2026-06-10 I caught the mismatch, compared it against the original proposal, and **pivoted back to the proposal's EM/ED-only PRISMA-ScR scoping review (RQ1–RQ3)**. The good news is that almost nothing from the detour is wasted — the strongest pieces carry over as upgrades to the corrected design, and the rest is intact in git history as a head start on later-semester work.

---

## 2. What I actually built first (the "optimistic" version)

While doing the foundational conceptual work — grounding definitions in the seven canonical XAI papers, drafting an inclusion boundary, building taxonomies and rubrics — the project organically expanded into:

- A **cross-domain** scope (all clinical AI applications, not just emergency medicine)
- A **PRISMA systematic review** with **6 pre-registered confirmatory hypotheses** (H1–H6) and 5 secondary research questions
- A **5-database search plan** (PubMed, Embase, CINAHL, IEEE Xplore, ACM Digital Library)
- A fully validated PubMed search string returning **9,672 hits** (2015–2024), plus draft translations to the other four databases
- Both an OSF pre-registration draft *and* a PROSPERO registration draft

This was real, careful work — the search string went through three documented diagnostic cycles and was validated against an independently citation-chased benchmark — but it is a different (and considerably larger) project than the one in the April proposal, which specifies an **EM/ED-only JBI scoping review** reported via **PRISMA-ScR**, structured around **RQ1–RQ3** with a regulatory-readiness framing, across **4 databases**.

---

## 3. The pivot (2026-06-10)

I compared the repo's built-out scope against the original proposal PDF and confirmed the divergence was real, not just a framing difference. Decision: **revert to the proposal's original scope** — EM/ED-only, RQ1–RQ3, JBI scoping methodology + PRISMA-ScR reporting, narrative synthesis by research question, 4 databases.

**Why now, and why this direction:**

1. **Capacity.** An 8-week, single-reviewer timeline cannot support a cross-domain corpus sized for confirmatory hypothesis testing (9,672 PubMed records alone) plus 4–5 database translations plus full extraction, IRR, synthesis, and manuscript drafting. The EM-narrowed corpus (~500 PubMed records) is the only configuration that's realistically completable in the remaining time.
2. **The grading rubric rewards the proposal's design, not the detour's.** Analysis & Synthesis is 25% of the grade and explicitly requires the synthesis to *argue, not summarize*. A narrative synthesis organized around RQ1–RQ3 with a regulatory-readiness argument fits that far better than reporting results across 6 hypotheses — two of which (H4, H6) were already at risk of underpowered cells even in the larger corpus.
3. **Timeliness.** The regulatory framing (FDA AI/ML guidance, EU AI Act Article 13 — a 2024 regulation) is novel and gives the EM-narrowed scope a stronger publication hook than the broad cross-domain framing did.
4. **It matches the proposal's own framing.** The proposal explicitly describes this review as "scaffolding for the empirical studies planned in later semesters" — which is exactly the role the parked cross-domain work can now play.

---

## 4. What carries forward as upgrades (not wasted)

Several constructs developed during the detour are *more rigorous* than what the original proposal specified, and slot directly into the EM-only design:

| From the detour | Role in the corrected (EM) design |
|---|---|
| Trust-calibration vs. explanation-plausibility distinction (Issue #3) | Sharpens the proposal's single "trust calibration" construct; feeds RQ3 |
| 4-dimension ecological validity rubric (Issue #5) | Secondary/exploratory lens on RQ2's evaluation-rigor question |
| Workflow realism rubric (Issue #4) + 5-dimension quality rubric QR1–QR5 (Issue #20) | Repositioned as supplementary analyses feeding the RQ2 narrative |
| 6-type evaluation taxonomy mapped to Doshi-Velez & Kim (2017) (Issue #8) | Becomes the operational basis for RQ1/RQ2/RQ3 framework classification |
| 21-tag controlled vocabulary (Issue #13) | Retained as-is for coding |
| OSF pre-registration (filed 2026-05-24) | Retained as the registration record; rewritten as v2 for EM scope |

---

## 5. What's parked for later (kept, not discarded)

The cross-domain build-out is preserved in git history rather than deleted, exactly as the proposal anticipated:

- Cross-domain 6-hypothesis framing (H1–H6) and the 5 secondary research questions
- The validated cross-domain PubMed string (9,672 hits, 2015–2024) and its diagnostic/validation trail
- Draft cross-domain translations for Embase, CINAHL, IEEE Xplore, and ACM
- The 5-database search plan (CINAHL specifically — dropped from the EM-only primary search since its nursing/allied-health focus mapped to the broader population scope)
- PROSPERO draft (Issue #19) — paused rather than submitted, since OSF is the registration the proposal requires

This is the natural starting point if a future semester takes on the full cross-domain systematic review.

---

## 6. Where the EM-only review stands right now

- **Inclusion boundary v2** (3-gate EM-only rule: ED-encounter decision point → XAI/interpretable method → empirical evaluation) finalized 2026-06-10
- **PubMed search string v2** finalized as Concept A (XAI) AND Concept B (clinical context) AND Concept C (ED/triage/ESI/acuity/disposition), with the date range extended to a rolling "2015 through search-execution date" window: **213 hits (2015–2024) / 497 hits (2015–2026-06-10)**
- Embase, IEEE Xplore, and ACM translations re-derived for the EM scope; CINAHL shelved
- Extraction schema extended to v1.3 (10 new columns covering RQ1 method-justification coding and RQ3's four regulatory-evidence criteria)
- Screening criteria and a supplementary search/provenance plan (Rayyan/Elicit/Google Scholar) drafted
- As a pre-screening QC step, 11 retracted PubMed records were identified and logged (one notable finding: a cluster traces to the 2023 Hindawi mass-retraction event — flagged as a candidate limitations-section observation)

**In progress:** assembling an EM-specific recall benchmark (the cross-domain benchmark doesn't transfer to the narrower scope) to validate the 213/497-hit string before formal execution.

---

## 7. Immediate next steps

1. Finish the EM-specific recall benchmark and validate the A+B+C string against it
2. Formally execute all 4 databases on the same date; export raw results to `data/searches/`
3. Update `prisma_counts.csv` Identification rows with the EM-narrowed counts
4. Begin title/abstract screening in Rayyan

---

## 8. Schedule impact

Phase 1 is running slightly past its proposed Week 1–3 window because of the detour and pivot. However, the corrected scope (~500 PubMed records vs. ~9,672+ across five databases) is substantially lighter than what I was on track to screen otherwise, so I expect this to net out close to neutral — and likely faster — for the overall 8-week timeline. I'll flag immediately if the EM-specific recall benchmark or full execution surfaces anything that changes that assessment.

---

## 9. Bottom line

The first three weeks produced a more ambitious review than the one that was approved. I caught it before it consumed search-execution or screening time, the most rigorous conceptual work from that period upgrades the corrected design rather than being discarded, and the broader version remains intact in git history as a documented starting point for later-semester work — which is the role the proposal already envisioned for follow-on empirical studies. Flagging this now in case you'd like to weigh in on the scope before I move into title/abstract screening.
