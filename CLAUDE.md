# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

This repository is for a clinical XAI (Explainable AI) review project (reference: 9970).

## Repository Structure

| Path | Purpose |
|------|---------|
| `docs/protocol/` | Review protocol |
| `docs/osf/` | OSF registration materials |
| `docs/manuscript/` | Manuscript drafts |
| `docs/figures/` | Figures for publication |
| `docs/supplementary/` | Supplementary materials |
| `data/searches/` | Raw search results |
| `data/screening/` | Title/abstract and full-text screening |
| `data/extraction/` | Data extraction forms and outputs |
| `data/coding/` | Coding schemes and coded data |
| `data/synthesis/` | Synthesis outputs |
| `notebooks/` | Analysis notebooks |
| `scripts/` | Data processing scripts |
| `references/bib/` | Bibliography files |
| `references/annotated/` | Annotated references |
| `memos/` | Research memos |
| `project_management/milestones/` | Project milestones |
| `project_management/weekly_logs/` | Weekly progress logs |
| `project_management/reviewer_risks/` | Reviewer risk tracking |

## Writing Style

Before finalizing any prose destined for a document in this repo (manuscript drafts, protocol text, OSF registration materials, memos, or any other narrative/prose content meant to be read as authored text rather than code or data) — invoke the `humanizer` skill on the draft to strip AI-writing tells (em dash overuse, rule-of-three, inflated symbolism, hedging/filler phrases, etc.) before presenting or committing it.

## Getting Started

This is a fresh repository. When the project is initialized, document here:
- How to install dependencies
- How to run the project
- How to run tests
- How to lint/format code
