# Extraction Tracker — 7 Included Studies

Tracks per-paper extraction status against the 43-column schema (`schema_v1.csv` / `schema_README.md`). Source PDFs live in `data/extraction/fulltext_pdfs/` (already present, no need to keep separate copies elsewhere).

| # | Rayyan file | PaperID | Zotero_Key | Status | Rationale file |
|---|-------------|---------|------------|--------|-----------------|
| 1 | `rayyan-601300063.pdf` | Sulaiman_2025 | *(pending — reviewer supplies)* | Confirmed (in schema_v1.csv), Zotero_Key still open | `per_paper/601300063.md` |
| 2 | `rayyan-601300068.pdf` | Sulaiman_2023 | *(pending — reviewer supplies)* | Confirmed (in schema_v1.csv), Zotero_Key still open | `per_paper/601300068.md` |
| 3 | `rayyan-601300083.pdf` | Arnaud_2023 | *(pending — reviewer supplies)* | Confirmed (in schema_v1.csv), Zotero_Key still open | `per_paper/601300083.md` |
| 4 | `rayyan-601300366_PMC12940882.pdf` | Juang_2026 | *(pending — reviewer supplies)* | Confirmed (in schema_v1.csv), Zotero_Key still open | `per_paper/601300366.md` |
| 5 | `rayyan-601300391.pdf` | Xie_2021 | *(pending — reviewer supplies)* | Confirmed (in schema_v1.csv), Zotero_Key still open | `per_paper/601300391.md` |
| 6 | `rayyan-601300407_PMC12602473.pdf` | Han_2025 | *(pending — reviewer supplies)* | Confirmed (in schema_v1.csv), Zotero_Key still open — 2 fields corrected for cross-paper consistency | `per_paper/601300407.md` |
| 7 | `rayyan-601300595.pdf` | Tang_2026 | *(pending — reviewer supplies)* | Confirmed (in schema_v1.csv), Zotero_Key still open | `per_paper/601300595.md` |

**Status values:** `Not started` → `Drafted (pending review)` → `Confirmed (in schema_v1.csv)`

## Workflow per paper

1. Ask the `extractor` subagent to extract one paper, giving it the path under `data/extraction/fulltext_pdfs/`.
2. It returns a schema-ordered CSV row plus an evidence writeup grouped by section, and flags anything uncertain.
3. Save the evidence writeup to this paper's rationale file under `data/extraction/per_paper/` (create the directory on first use).
4. Review the row — resolve flagged uncertainties, fill in `Zotero_Key` from your reference manager, adjust any call you disagree with.
5. Append the confirmed row to `schema_v1.csv` (header order must match exactly).
6. Update this tracker's Status and PaperID/Zotero_Key columns.

Once all 7 rows are confirmed, `schema_v1.csv` is complete and the Results-chapter tables (per `docs/manuscript/chapter_plan_v1.md`) can be built directly from it.

## Notes

- `DoshiVelez_Category` and `VilonLongo_Category` are independent axes — expect them to disagree with each other sometimes; that's not an error, they measure different things (see `schema_README.md`).
- **Tie-break rule (2026-07-23):** if `Eval_Type=None` but `N_Participants>0` (informal, sub-taxonomy-threshold human involvement), code `DoshiVelez_Category=FunctionallyGrounded` and flag it — see `memos/decision_log.md` 2026-07-23 entry and `schema_README.md`.
- **`Domain` has no `EmergencyMedicine` value (2026-07-23, kept as-is):** `Han_2025`=`EHR`, `Tang_2026`=`Other` for ED-specific studies — accepted inconsistency since the whole review is ED-scoped already. See `memos/decision_log.md`.
- The four `Reg_*` columns default to `No` in the absence of explicit tested evidence — don't let a paper's future-work language push one to `Yes`.
- If a genuinely new `Tags` value seems needed, log it in `memos/decision_log.md` before using it (per the controlled-vocabulary rule).
