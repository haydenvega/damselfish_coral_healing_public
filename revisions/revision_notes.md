# Revision Notes — Biology Letters RSBL-2026-0177

Technical notes on the analysis-code changes made in response to peer review (minor revision, May 2026). This document explains what changed in the analysis pipeline and why. The reviewer comments themselves and the formal response to reviewers are not included in this repository.

For the headline test statistics, see the regenerated HTMLs in `analysis_visualization_code/`. For reproducibility, the full pipeline can be re-run with the original instructions in the top-level `README.md`.

---

## 1. Explicit ML fitting of all mixed-effects models (Reviewer 1)

**Change:** Every `lme4::lmer()` call across the three Rmds now sets `REML = FALSE` explicitly.

**Files changed:**

- `analysis_visualization_code/wound/wound_closure_analysis.Rmd` — 4 model fits (`fit-healing-models` chunk)
- `analysis_visualization_code/photo_eff/pam_analysis.Rmd` — 4 model fits in `fit-fvfm-models` and 3 in `test-algae-effect`
- `analysis_visualization_code/growth/allometric_growth_analysis.Rmd` — 5 model fits in `fit-growth-rate-models` (the ANCOVA model in `fit-allometric-model` was already correct)

**Why:** Likelihood ratio tests comparing nested fixed-effect structures are only valid when the underlying models are fit by maximum likelihood, not restricted maximum likelihood. Previously, some models used `lme4::lmer()`'s default (`REML = TRUE`), so we made the ML fitting explicit.

**Impact:** None on inference. `lme4::anova()` silently refits both compared models with ML internally, so the previously reported test statistics were already computed correctly. The change is a documentation/best-practice fix that makes the intent of the code unambiguous to a future reader.

---

## 2. Left-censoring documentation for healing rate (Reviewer 1)

**Change:** New section 6b in `wound_closure_analysis.Rmd` documents the proportion of wounded fragments that reached complete closure (`wound_size_final = 0`) before day 21.

**Result:** 25 of 48 wounded fragments fully closed by day 21:

| Treatment | Closed | Open | % closed |
|---|---|---|---|
| No Fish / Small | 6 | 5 | 55% |
| No Fish / Large | 3 | 9 | 25% |
| Fish / Small | 8 | 4 | 67% |
| Fish / Large | 8 | 4 | 67% |

**Why:** When a wound closes before the measurement endpoint, the simple rate `(initial − final) / 21 d` underestimates the true healing speed for that fragment. The reviewer asked whether this affected the interpretation.

**Interpretation:** Censoring is concentrated in the fish-present cells (67% censored) and rarest in the No Fish / Large cell (25%) — i.e., the bias runs *against* the fish effect, not for it. The reported fish × wound interaction is therefore conservative. A censoring-aware estimator (e.g., a Cox or interval-censored model on a full daily time series) would return a larger fish × wound effect, not smaller.

We do not refit a censored-regression model because the full day-of-closure series exists only for the daily-photographed subset (one fragment per wound × tank). A future replication with daily photography of every fragment would enable this.

---

## 3. Fisher's exact test for turf-algae persistence (Reviewer 1)

**Change:** New section 6c in `wound_closure_analysis.Rmd` runs a Fisher's exact test on the 2 × 2 contingency of fish treatment × turf-algae persistence at day 21, restricted to the 48 wounded corals.

**Data:**

|  | Algae persisted | Algae cleared | Total |
|---|---|---|---|
| No Fish | 7 | 17 | 24 |
| Fish | 1 | 23 | 24 |

**Result:** Odds ratio = 0.11 (95% CI: 0.00–0.99), p = 0.048. The odds of turf-algae persistence in no-fish tanks were ~9× the odds in fish tanks.

**Why:** This result had previously been reported parenthetically. The reviewer asked for a formal test. The Fisher's exact is appropriate for the small expected cell counts (the chi-square approximation would be poor).

**Caveat (now also added to the manuscript Discussion):** The design cannot distinguish two non-mutually-exclusive mechanisms — (a) direct exclusion of turf algae by *Dascyllus* through territorial grazing or aggression, and (b) faster wound closure in fish-present treatments shortening the window of substrate availability for algal colonization. Both pathways predict the observed pattern. Future work that decouples the fish presence from the healing-rate trajectory (e.g., fish present briefly then removed) could resolve their relative contribution.

---

## 4. Fv/Fm sensitivity analysis excluding algae-colonized corals (Reviewer 1)

**Change:** New section 3b in `pam_analysis.Rmd` does three things:

1. Reports group means for algae-colonized vs non-colonized corals.
2. Provides the tank-by-treatment distribution of the 8 algae-colonized fragments.
3. Refits the primary Fv/Fm model (`fv_fm ~ fish * wound + (1 | tank)`) excluding the 8 algae+ corals.

**Group means:**

- Algae+ (n = 8): mean Fv/Fm = 0.609 (95% CI: 0.582–0.636).
- Algae- (n = 64): mean Fv/Fm = 0.677 (95% CI: 0.672–0.683).

The ~0.07-unit gap is substantial and we had underappreciated it in the original manuscript.

**Tank distribution of algae+ fragments:**

| Tank | Fish | Wound | n |
|---|---|---|---|
| 2 | No Fish | Large | 4 |
| 3 | Fish | Small | 1 |
| 4 | No Fish | Large | 2 |
| 5 | No Fish | Small | 1 |

7 of 8 algae+ fragments are in no-fish tanks; 6 of 8 have large wounds; all 8 sit in just 4 of the 6 tanks.

**Sensitivity result (n = 64):** Fish × wound interaction holds: χ²₂ = 10.248, p = 0.006 (compare primary n = 72: χ²₂ = 10.898, p = 0.004). Estimated cell means shift by ≤ 0.018 Fv/Fm units across all six cells. The pattern — depressed Fv/Fm in wounded corals without fish, preserved Fv/Fm in wounded corals with fish — survives the exclusion.

**Why:** The reviewer flagged that the original justification for pooling algae+ and algae- corals (a non-significant algae effect at p = 0.106) was weak: the algae+ sample is small (n = 8) and confounded with the treatments (7/8 in no-fish, 6/8 in large wounds), so the non-significance could easily reflect low power rather than no effect. The right defense is a sensitivity analysis, which this section now provides. The methods text in the manuscript was rewritten to reference the sensitivity analysis as the justification for pooling.

---

## 5. Other code-pipeline changes

- HTML reports re-knit from the updated Rmds (`*.html` in each analysis subdirectory).
- Figures regenerated to match the updated model fits and added analyses (all files in `figures/`).
- No changes to data, factor coding, or model structure beyond what is documented above.

---

## Reproducibility

Re-running the pipeline from a clean clone produces the same outputs:

```bash
cd damselfish_coral_healing_public
Rscript -e 'rmarkdown::render("analysis_visualization_code/wound/wound_closure_analysis.Rmd")'
Rscript -e 'rmarkdown::render("analysis_visualization_code/photo_eff/pam_analysis.Rmd")'
Rscript -e 'rmarkdown::render("analysis_visualization_code/growth/allometric_growth_analysis.Rmd")'
```

Required packages are listed in the top-level `README.md`.
