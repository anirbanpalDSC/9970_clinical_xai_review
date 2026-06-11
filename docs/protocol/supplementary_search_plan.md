# Supplementary Search and Provenance Plan

**Issue:** #23
**Status:** Draft
**Related:** `docs/osf/preregistration_draft.md` Section 4 (Databases and Search), `docs/protocol/search_string_pubmed_v1.md`, `docs/protocol/screening_criteria.md` (Issue #17), `data/screening/prisma_counts.csv`

## 1. Purpose

The four primary databases (PubMed/MEDLINE, Embase, IEEE Xplore, ACM Digital Library) form the core of the search strategy, but per JBI scoping review guidance (Peters et al., 2020) and PRISMA-ScR reporting (Tricco et al., 2018), scoping reviews are expected to supplement database searches with additional sources to mitigate two known gaps:

1. **Terminology drift** - clinical XAI papers use inconsistent terminology (`memos/terminology_instability.md`, Issue #2); a Boolean search string, however well-tuned, can miss papers that describe an interpretable triage model without using "explainable AI" / "XAI" language.
2. **Indexing lag** - preprints and very recent work may not yet be indexed in the primary databases at the time of the initial search.

This plan documents three supplementary channels - **Rayyan** (screening/deduplication/provenance), **Elicit** (semantic search per research question), and **Google Scholar** (citation tracing + grey literature/preprints) - and how each is logged and reported.

## 2. Rayyan - Deduplication, Screening, and Provenance

- All records from the four primary databases, plus all candidates surviving initial relevance triage from Elicit and Google Scholar (Sections 3-4), are imported into a single Rayyan review.
- Each record is tagged on import with a **source label** identifying its discovery channel:

| Source label | Meaning |
|---|---|
| `source:pubmed` | PubMed/MEDLINE primary search |
| `source:embase` | Embase primary search |
| `source:ieee` | IEEE Xplore primary search |
| `source:acm` | ACM Digital Library primary search |
| `source:elicit` | Elicit semantic search (Section 3) |
| `source:gscholar-fwd` | Google Scholar forward citation tracing (Section 4) |
| `source:gscholar-bwd` | Google Scholar backward citation tracing (Section 4) |
| `source:gscholar-greylit` | arXiv/SSRN grey-literature search (Section 4) |

- Rayyan's built-in deduplication is run across the merged corpus. When a duplicate spans multiple source labels, all labels are retained on the surviving record - this preserves the "found via N sources" information needed for the Identification-stage PRISMA-ScR count.
- Title/abstract and full-text screening proceed within Rayyan per `docs/protocol/screening_criteria.md` (Issue #17) and `docs/protocol/inclusion_boundary.md` (v2), regardless of source label - supplementary-source records are screened against the same three-gate inclusion boundary as primary-database records, with no relaxed criteria.
- PRISMA-ScR flow counts at each stage are exported from Rayyan and recorded in `data/screening/prisma_counts.csv`.

## 3. Elicit - Semantic Search per Research Question

Elicit (elicit.com) is used for natural-language semantic search, run as three separate queries - one framed around each of RQ1-RQ3 (`docs/osf/preregistration_draft.md` Section 2) - to surface papers that a Boolean keyword string would miss due to terminology drift.

For each query, the following is logged in `data/searches/elicit_query_log.csv` (created when the search is run):

| Column | Description |
|---|---|
| `Query_ID` | Sequential identifier (E1, E2, E3, ...) |
| `RQ` | Which research question framed the query (RQ1/RQ2/RQ3) |
| `Query_Text` | Exact natural-language query submitted to Elicit |
| `Date_Run` | Date the query was executed |
| `N_Results_Reviewed` | Number of ranked results reviewed (cutoff: top 50 by relevance, or fewer if relevance drops off sharply) |
| `N_Passed_Triage` | Number passing an initial relevance triage (clearly EM/ED + XAI related) |
| `Notes` | Any observations (e.g., recurring terminology not in the Boolean string) |

Records passing initial triage are imported into Rayyan tagged `source:elicit` and screened identically to primary-database records (Section 2).

## 4. Google Scholar - Citation Tracing and Grey Literature

### 4.1 Forward and backward citation tracing

Conducted **once, after full-text screening of the primary + Elicit corpus is complete** (to avoid redundant tracing of papers that are ultimately excluded):

- **Forward tracing:** for each study included after full-text screening, review Google Scholar's "Cited by" list for newer papers that might meet the inclusion criteria.
- **Backward tracing:** hand-search the reference lists of included studies for earlier relevant papers not captured by the database search.

### 4.2 Grey literature and preprints

Targeted search of **arXiv** (cs.AI, cs.LG, cs.HC categories) and **SSRN** for EM/XAI preprints not yet indexed in the primary databases, using the Concept A (XAI) + Concept C (ED/triage) terms from `docs/protocol/search_string_pubmed_v1.md`, adapted to each platform's search syntax.

### 4.3 Logging

Logged in `data/searches/gscholar_citation_log.csv` (created when the search is run):

| Column | Description |
|---|---|
| `Seed_PaperID` | PaperID of the included study used as the citation-tracing seed (forward/backward only; blank for grey-lit) |
| `Direction` | Forward / Backward / GreyLit |
| `Date_Run` | Date the search was executed |
| `N_Candidates_Reviewed` | Number of citing/cited/grey-lit candidates reviewed |
| `N_Passed_Triage` | Number passing initial relevance triage |
| `Notes` | Observations |

Records passing triage are imported into Rayyan tagged `source:gscholar-fwd`, `source:gscholar-bwd`, or `source:gscholar-greylit` as appropriate, and screened identically to primary-database records.

## 5. PRISMA-ScR Reporting

Per Tricco et al. (2018), supplementary-source records are reported as a distinct "Identification - other sources" stream in the PRISMA-ScR flow diagram, alongside the database-search stream. The existing row in `data/screening/prisma_counts.csv`:

```
Identification,Records from other sources (hand search / citation tracking),,
```

is populated with the combined total of Elicit + Google Scholar candidates passing initial triage (post-Rayyan-dedup against the primary-database set), once the supplementary searches are run.

## 6. Timing / Sequencing

| Phase | Activity |
|---|---|
| Phase 1 (weeks 1-3) | Primary database searches (PubMed/Embase/IEEE/ACM, EM-narrowed v2 string) and the three Elicit queries run together; all records imported into Rayyan, deduplicated, and title/abstract-screened as one corpus. |
| Phase 2 (weeks 4-6) | After full-text screening of the primary + Elicit corpus, run Google Scholar forward/backward citation tracing on the included set, plus the arXiv/SSRN grey-literature search. New candidates undergo an abbreviated screening pass (title/abstract + full-text) before final inclusion. |
| Phase 3 (weeks 7-8) | The January-2025-onward update search (`docs/osf/preregistration_draft.md` Section 10) re-runs Concept A+C across the 4 primary databases. Elicit and Google Scholar supplementary steps are not repeated for the update unless time permits. |

## Version History

| Version | Date | Changes |
|---|---|---|
| Draft v1 | 2026-06-10 | Initial draft, created as part of the EM-pivot (`memos/decision_log.md`, 2026-06-10, "What changes" - supplementary search/provenance plan). Issue #23. |
