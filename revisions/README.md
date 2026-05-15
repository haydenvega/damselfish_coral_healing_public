# Revisions

Documents related to peer review and revision of the manuscript.

## Contents

- **`response_to_reviewers.md`** — working draft of the response to reviewers for the Biology Letters submission (RSBL-2026-0177). `[TBD: …]` markers identify line numbers and field details that will be finalized before submission.
- **`how_to_respond_to_reviewers.md`** — a short primer on the craft of writing peer-review responses. Developed during this revision; principles generalize to other papers.

`.docx` versions of each are provided for convenience.

## Corresponding code changes

The new analyses requested by Referee 1 live in the main analysis Rmds:

- `analysis_visualization_code/wound/wound_closure_analysis.Rmd`
  - Section 6b — left-censoring cross-tab (R1.2)
  - Section 6c — Fisher's exact test for turf-algae persistence (R1.4)
- `analysis_visualization_code/photo_eff/pam_analysis.Rmd`
  - Section 3b — Fv/Fm sensitivity analysis excluding algae-colonized corals (R1.3)

All `lmer()` calls across the three Rmds were also explicitly refit with `REML = FALSE` for fixed-effect LRT validity (R1.1). Inference was preserved.
