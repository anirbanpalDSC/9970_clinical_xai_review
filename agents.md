# agents.md

Agent instructions for the **Clinical XAI Systematic Review** project (ref: 9970).
This file governs how AI agents and collaborators work in this repository.

---

## Repository Structure

```
Clinical_XAI_Review/
│
├── 00_Admin/           # IRB, OSF registration, team agreements, changelog
├── 01_Protocol/        # PRISMA-P, pre-registration, eligibility criteria
├── 02_Search_Strategy/ # Database queries, PICO/SPIDER frames, search logs
├── 03_Seed_Papers/     # Foundational papers that anchor the review scope
├── 04_Screening/       # Title/abstract and full-text screening records
├── 05_Extraction/      # Data extraction templates and completed forms
├── 06_Frameworks/      # XAI framework comparisons and taxonomy drafts
├── 07_Synthesis/       # Evidence tables, meta-analysis, narrative synthesis
├── 08_Figures/         # All figures (source files + exported PNGs/SVGs)
├── 09_Manuscript/      # Draft sections, revision history, submission files
├── 10_References/      # Exported .bib files, Zotero RDF exports
└── 11_Research_Memos/  # Daily/weekly research memos and decision logs
```

Never flatten this structure. Every file must live in its correct folder.

---

## Git Best Practices

### Commits

- Write commits in the **imperative mood**: `Add`, `Update`, `Fix`, `Remove`, `Refactor`.
- Keep the subject line under **72 characters**.
- Reference the relevant phase/folder in the message: `[05_Extraction] Add inter-rater reliability sheet`.
- Commit **one logical change** per commit — do not bundle unrelated changes.
- Never commit binary files (PDFs, `.docx`) without explicit instruction. Use Git LFS or store references instead.
- Never commit credentials, API keys, or personal identifiers.

**Commit message format:**
```
[folder_tag] Short imperative summary (≤72 chars)

Optional: 1–3 lines explaining WHY, not WHAT.
```

Examples:
```
[01_Protocol] Draft PRISMA-P eligibility criteria section
[05_Extraction] Fix trust calibration column mapping in template
[11_Research_Memos] Append memo 2026-05-17: interpretability conflicts
```

### What to commit

| Always commit | Never commit |
|---|---|
| `.md`, `.tex`, `.bib`, `.csv`, `.json` | PDFs, Word `.docx` files |
| Data extraction templates | Raw Zotero library exports (use `.bib` only) |
| Figures (SVG/PNG ≤ 5 MB) | API keys, OSF tokens |
| Search query logs | Intermediate Rayyan exports unless finalized |

---

## Branching Strategy

This is a **solo research project**. Use a lightweight branching model:

### Permanent branches

| Branch | Purpose |
|---|---|
| `main` | Stable, peer-reviewable state. Every merge here = a milestone. |
| `develop` | Active daily work. Merge to `main` at phase completions. |

### Short-lived feature branches

Create a branch per discrete task. Delete after merging.

**Naming convention:**
```
<phase>/<short-description>
```

Examples:
```
protocol/eligibility-criteria
search/pubmed-query-v2
extraction/trust-calibration-coding
synthesis/evidence-table-draft
manuscript/discussion-xai-frameworks
memo/weekly-2026-05-17
```

### Workflow

```
main
 └── develop
      ├── protocol/eligibility-criteria   ← merge back to develop when done
      ├── extraction/template-v2
      └── manuscript/intro-draft
```

1. Branch from `develop`, never from `main`.
2. Open a PR (or merge with a descriptive message) into `develop` when work is complete.
3. Merge `develop` → `main` only at **phase milestones** (e.g., protocol locked, screening complete, extraction complete, manuscript submitted).
4. Tag milestones on `main`:

```
git tag -a v0.1-protocol-registered -m "PROSPERO/OSF registration complete"
git tag -a v0.2-screening-complete  -m "Full-text screening finalized, n=XX included"
git tag -a v0.3-extraction-complete -m "Data extraction locked, ready for synthesis"
git tag -a v1.0-submission          -m "Manuscript submitted to journal"
```

---

## Citation Infrastructure

| Purpose | Tool |
|---|---|
| Reference manager | Zotero |
| PDF annotation | Zotero built-in + PDF Expert / Drawboard |
| Title/abstract screening | Rayyan |
| Semantic discovery & gap-finding | Elicit |
| Citation tracing (forward/backward) | Google Scholar |
| Structured data extraction | Airtable / Notion / Google Sheets |
| Protocol hosting & pre-registration | OSF |
| Writing | Overleaf (LaTeX) or Markdown + Pandoc |

### Zotero conventions

- All papers must be tagged with their **review phase**: `seed`, `screened-in`, `excluded-ft`, `included`.
- Use a consistent collection hierarchy mirroring the folder structure above.
- Export `.bib` to `10_References/` whenever the library is updated.

---

## Master Research Memo

Maintained at: `11_Research_Memos/research_master_memo.md`

**Append an entry every working day** using this template:

```markdown
## YYYY-MM-DD

### Insights
-

### Contradictions
-

### Terminology Conflicts
-

### Recurring Themes
-

### Methodological Weaknesses
-

### Candidate Figures
-

### Synthesis Hypotheses
-
```

This memo is the intellectual backbone of the Discussion section. Do not overwrite previous entries — always append. Agents must read the most recent entry before making synthesis or extraction decisions.

---

## Core Definitions Table

These definitions are **locked working definitions** for this review. All extraction, coding, and synthesis must use these consistently. If a source uses a term differently, note the conflict in the memo — do not silently override the definition.

| Construct | Working Definition | Citation Basis |
|---|---|---|
| **Interpretability** | The degree to which a human can understand the internal mechanism of a model — its structure, parameters, or decision logic — without requiring post-hoc explanation. | TBD |
| **Explainability** | The degree to which a model's outputs or predictions can be made comprehensible to a target audience via post-hoc techniques (e.g., SHAP, LIME, attention maps). | TBD |
| **Trust calibration** | The alignment between a clinician's confidence in an AI system's outputs and the system's actual accuracy or reliability; calibrated trust = neither over-reliance nor under-reliance. | TBD |
| **Clinical usability** | The extent to which an XAI output can be acted upon within real clinical workflows — accounting for time constraints, interface design, and cognitive load. | TBD |
| **Evaluation validity** | The extent to which an XAI evaluation metric or study design measures what it claims to measure in a clinically meaningful way. | TBD |
| **Workflow realism** | The degree to which a study's experimental conditions reflect actual clinical practice (staffing, time pressure, EHR context, patient mix). | TBD |
| **Ecological validity** | Broader than workflow realism: the extent to which findings generalize to real-world clinical settings across institutions, populations, and care contexts. | TBD |
| **Transparency** | A property of the overall AI system (not just the model) — the degree to which its design, data, training, and limitations are disclosed to users and stakeholders. | TBD |
| **Reliance** | Behavioral outcome: the extent to which a clinician follows an AI recommendation, whether appropriate (correct reliance) or inappropriate (over/under-reliance). | TBD |
| **Fidelity** | The degree to which an explanation accurately reflects the model's actual reasoning process, as opposed to being a plausible but unfaithful approximation. | TBD |

**Disambiguation note:** Interpretability and Explainability are treated as distinct constructs in this review. Papers that conflate them should be flagged in extraction under `terminology_conflict = TRUE`.

---

## Agent Behavioral Rules

1. **Read `research_master_memo.md` before any synthesis task.** Do not derive conclusions the memo has already revised or contradicted.
2. **Do not rename or move files** without updating both `CLAUDE.md` and this file.
3. **Do not modify the Definitions Table** without appending a dated rationale entry to the memo and getting explicit user confirmation.
4. **All extraction work** must use the template in `05_Extraction/` — never create ad-hoc extraction formats.
5. **Figures** must be saved in both editable source format and exported PNG/SVG in `08_Figures/`.
6. When uncertain about inclusion/exclusion of a paper, **flag it for human review** — do not decide unilaterally.
