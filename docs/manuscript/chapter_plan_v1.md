# Chapter Plan — 9970 Clinical XAI Scoping Review

**Mode:** academic-paper `plan` (v3.2.0)
**Date:** 2026-07-22
**Status:** Provisional pending extraction/synthesis of the 7 included studies — RQ2/RQ3 claims are framed as expectations to test, not findings, until then.

---

## Paper Configuration Record (Plan Mode)

| Parameter | Value |
|-----------|-------|
| **Topic** | 9970 clinical XAI scoping review — post-hoc XAI methods in emergency medicine |
| **Structure** | PRISMA-ScR scoping review format (not classic IMRaD) |
| **Existing Materials** | Finalized preregistration/protocol; screening complete (7 included studies); 7 full-text PDFs in `Downloads/review` awaiting extraction; extraction schema exists (`data/extraction/schema_v1.csv`, 43 cols) but `VilonLongo_Category` vocabulary needs pilot verification before use |
| **Target length** | ~5,000–6,000 words (body), typical for a PRISMA-ScR scoping review manuscript at this scope |

---

## Core Argument

**Thesis (provisional, pending extraction):** EM clinical XAI research has proliferated post-hoc explanation methods whose selection is rarely justified and whose effectiveness is rarely tested beyond how plausible the explanation looks, leaving a field that appears mature but would not currently satisfy the evidentiary bar emerging regulatory frameworks are starting to set for interpretability validation.

**Contribution claim:** This paper establishes a narrower, EM-specific finding — that current EM-XAI evaluation practice does not yet produce governance-compliant, effective XAI methods — and its contribution is to bring governance considerations into EM-XAI development earlier, rather than as a retrofit after methods are already built and deployed.

**Framing discipline agreed during stress-testing:** claims are descriptive ("the evidence gap suggests governance is currently arriving too late"), not causal ("earlier governance would have fixed it") — the 7-paper corpus can support the former, not the latter. The counter to "governance can't engage this early" is that FDA SaMD guidance and EU AI Act Art. 13 are already setting expectations pre-deployment, so "too early" isn't an available objection.

**RQ weighting:** RQ2 (evaluation rigor) supplies the evidentiary core; RQ3 (regulatory readiness) supplies the contribution/novelty; RQ1 (methods/justification) is descriptive scaffolding for both.

---

## Chapter-by-Chapter Plan

### Introduction (~800 words)
- **Urgency:** clinical stakes first (ED clinicians already handed unvalidated explanations under time/cognitive pressure) → pivot to regulatory clock (FDA SaMD, EU AI Act Art. 13 expectations rising now)
- **Gap:** no existing review examines whether EM-specific XAI evaluation evidence would satisfy emerging regulatory interpretability-validation expectations — gap claim rests on a search of prior *reviews*, independent of this review's own n=7
- **Evidence:** RQ1–RQ3 stated; interpretability-validity framework (interpretability / trust calibration vs. plausibility / evaluation validity) introduced here

### Background / Related Work — folded into Introduction per PRISMA-ScR convention (~700 words)
- Three-story structure: (a) generic/technical XAI-methods reviews with no clinical grounding, (b) broad clinical-XAI reviews not EM-specific, (c) EM-specific AI/ML reviews not XAI-focused — converging on the unclaimed EM + XAI + regulatory-mapping intersection
- No specific prior work identified to push back against by name (left open; optional verified-search follow-up if a foil is wanted later)
- Findings language will be scope-bound ("among the 7 studies meeting this review's inclusion criteria"), never generalized to "EM clinical XAI" as a whole; the small N is framed as a nascency finding, not apologized for

### Methods (~1,100 words)
- Funnel: 650 title/abstract records → borderline adjudication → 64 full-text assessed → 7 included, per the documented Gate 1/2/3 exclusion boundary
- Defense against "why not a broader clinical-XAI review": EM-specific narrowing is the contribution, not a limitation
- Extraction: 43-column schema (`data/extraction/schema_v1.csv`), mapped to RQ1 (`Method_Justification_Type/Notes`, `Method_Interface_Isolated`), RQ2 (`Eval_Type`, `Realism_Level`, `EV_*`, `DoshiVelez_Category`), RQ3 (`Reg_*`, `Trust_Claim/Trust_Only`, `VilonLongo_Category`)
- Limitations named directly: small final N (7) — reframed as evidence of field nascency; sole-reviewer design — accepted as appropriate scope for a solo project, not treated as a gap needing mitigation
- Synthesis approach: narrative synthesis by RQ (JBI/Peters 2020, PRISMA-ScR/Tricco 2018), not meta-analysis — justified by heterogeneity (7 papers vary in ED situation, XAI method, and evaluation type but share the explainability focus)

### Results (~1,400 words)
- Three subsections, one per RQ, each a charted table pulled directly from the extraction schema:
  - RQ1: XAI method family × justification type × EM decision category
  - RQ2: Eval_Type/DoshiVelez_Category distribution across the 5 evaluation levels, cross-tabulated with EV rubric
  - RQ3: proportion of studies meeting each of the four Reg_* criteria, with representative gaps
- Content here is genuinely pending — this section cannot be drafted until extraction is complete

### Discussion (~1,400 words)
- Literature dialogue: extend the known plausibility-vs-calibration concern (already established in prior conceptual work, not claimed as newly discovered) with EM-specific evidence; the regulatory connection (RQ3) is the actually-novel move
- Memorable takeaway (flexible pending data): "Explanations that satisfy clinicians are not automatically explanations that are safe to deploy — and the EM-XAI literature currently has little evidence that anyone has checked the difference."
- Recommendations:
  1. Reporting-standard proposal — future EM-XAI studies report against the four Reg_* criteria explicitly (akin to TRIPOD-AI/CONSORT-AI/DECIDE-AI)
  2. Design recommendation — isolate explanation-method effects from interface/presentation effects (`Method_Interface_Isolated`)
  3. Evaluation-tier push — move toward application-grounded evaluation before deployment/trust claims are made publicly
  4. Governance/policy close — absence of EM/ED-specific regulatory guidance despite general AI/ML SaMD frameworks; governance needs to enter earlier in the development process, not as a retrofit

### Conclusion (~400 words)
- One-paragraph close: explainability in EM should be standardized, policy-compliant, and effective — not merely plausible
- Future direction: this scoping review is explicitly scaffolding for the planned empirical, clinician-in-the-loop study referenced in the background section

---

## Open Items Before Full-Mode Drafting

1. **Run the `VilonLongo_Category` pilot** (verify provisional vocabulary in `data/extraction/schema_README.md` against Vilone & Longo, 2021, primary source) before extracting that column at scale.
2. **Extract all 7 papers** against the 43-column schema — Results and Discussion chapters cannot be drafted with real content until this is done.
3. **Optional:** verified literature search for a named prior work to push back against in the Background section (currently left open, not required).
4. Re-check the thesis and contribution claim against actual extraction results before drafting Discussion — both are explicitly conditional on the evidence per the user's own framing at Step 1.

---

## INSIGHT Collection

- **[INSIGHT: thesis_statement]** (provisional): EM clinical XAI research has proliferated post-hoc explanation methods whose selection is rarely justified and whose effectiveness is rarely tested beyond how plausible the explanation looks, leaving a field that appears mature but would not currently satisfy the evidentiary bar emerging regulatory frameworks are starting to set for interpretability validation — contingent on the 7 included studies bearing this out.
- **[INSIGHT: contribution_claim]**: This paper establishes a narrower, EM-specific finding — that current EM-XAI evaluation practice does not yet produce governance-compliant, effective XAI methods — and its contribution is to bring governance considerations into EM-XAI development earlier, rather than as a retrofit.
- **[INSIGHT: rq_weighting]**: RQ2 = evidentiary core, RQ3 = contribution/novelty, RQ1 = descriptive scaffolding.
- **[INSIGHT: framing_discipline]**: descriptive claims only ("governance arrives too late"), not causal ("earlier governance would have fixed it") — the corpus supports the former, not the latter.

---

## Next Step

Use `full` mode once extraction is complete to produce the complete draft, or `outline-only` mode now if a structural sanity check is wanted before extraction finishes. This Chapter Plan can also be handed to `academic-paper-reviewer` for a pre-drafting sanity review.
