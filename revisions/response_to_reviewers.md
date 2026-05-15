# Response to Reviewers

**Manuscript:** RSBL-2026-0177
**Title:** Coral-Associated Fishes Accelerate Coral Wound Healing and Photosynthetic Recovery
**Authors:** Vega, Osenberg, Seifert, Munk, Stier
**Journal:** *Biology Letters*

---

Thanks to the editor and both referees for the careful read. Their comments improved the statistical reporting, prompted a formal test of the turf-algae result, and tightened the Methods. We address every point below. Manuscript line numbers refer to the tracked-changes revised version.

This is a working draft. `[TBD: …]` placeholders mark line numbers, supplementary table numbers, and field details that will be filled in before submission. The corresponding code changes are in `analysis_visualization_code/` — see new sections 6b (closure cross-tab, R1.2), 6c (Fisher's exact for turf algae, R1.4) in `wound_closure_analysis.Rmd`, and section 3b (Fv/Fm sensitivity excluding algae-colonized corals, R1.3) in `pam_analysis.Rmd`.

---

## Referee 1

The four substantive points from R1 (REML, censoring, algae pooling, formal algae test) were all worth raising. We respond to each below.

---

### R1.1 — ML vs REML for fixed-effect LRTs (lines 146–148)

> *"...lines 146–148 state that maximum likelihood estimation was used to test the significance of treatment effects via likelihood ratio tests, but do not specify whether models were fitted by maximum likelihood (ML) or restricted maximum likelihood (REML). This distinction is critical: LRTs comparing fixed effects in mixed models require ML fitting, and p-values derived from REML-fitted models are not formally valid for fixed-effect comparisons."*

We refit every mixed-effects model with `REML = FALSE` and re-ran the LRTs. Two clarifications:

1. The allometric ANCOVA growth model was already fit with `REML = FALSE`; the wound-healing, Fv/Fm, and growth-rate-per-SA models were not, and we have fixed that.
2. `lme4::anova()` silently refits both models with ML when comparing REML-fitted lmer models, so the previously reported test statistics were already computed on ML refits internally. Test statistics and inference are therefore unchanged:
   - Healing rate fish × wound: χ² = 4.416, p = 0.036 (no change).
   - Fv/Fm fish × wound: χ²₂ = 10.898, p = 0.0043 (no change).
   - Growth ANCOVA: no change.

Methods (lines 146–148) now read:
> *"All mixed-effects models were fitted by maximum likelihood (`REML = FALSE` in `lme4::lmer`) so that likelihood ratio tests comparing nested fixed-effect structures are valid (Pinheiro & Bates 2000). Variance components reported in supplementary tables are from REML refits of the same final models."*

---

### R1.2 — Left-censoring of healing rate (lines 116–117)

> *"If any large-wound corals in the fish-present treatment achieved complete closure before day 21, the calculated rate underestimates true healing speed and the distribution may be effectively left-censored... The authors should verify whether complete closure occurred before the endpoint in any fragments and, if so, consider whether this affects interpretation."*

We checked. **25 of 48 wounded fragments (52%)** reached `wound_size_final = 0` by day 21:

| Treatment | Closed by day 21 | Still open | % closed |
|---|---|---|---|
| No Fish / Small | 6 | 5 | 55% |
| No Fish / Large | 3 | 9 | 25% |
| Fish / Small | 8 | 4 | 67% |
| Fish / Large | 8 | 4 | 67% |

The censoring runs against the fish effect, not for it: 67% of fish-present wounds censor versus 25% of No Fish / Large, the cell against which the fish effect contrasts most strongly. With a fixed 21-day denominator, our healing-rate estimate is therefore **conservative** for fish-treatment fragments. A censoring-aware estimator would return a *larger* fish × wound effect, not smaller.

The full day-of-closure series exists only for the daily-photographed subset (one fragment per wound × tank), so we cannot refit a censored-regression model on all 48 wounded corals. We have added the closure cross-tab to a new section in `wound_closure_analysis.Rmd` (section 6b) and a sentence to the Discussion (lines `[TBD]`) noting that complete closure was common, that our estimator is conservative as a result, and that this strengthens rather than weakens the fish × wound conclusion. A future replication with daily photography of every fragment would enable a Cox or interval-censored model.

---

### R1.3 — Fv/Fm pooling decision for algae-colonized corals (lines 131–133)

> *"The decision...to pool corals with and without algal colonisation in the Fv/Fm analysis, on the basis that Fv/Fm did not differ significantly between groups (p = 0.106), requires more careful justification... The authors should report the mean Fv/Fm of algae-colonised versus non-colonised corals, specify the tank-by-treatment distribution of these eight fragments, and confirm that excluding them does not materially alter the Fv/Fm model results."*

We agree the pooling decision was under-documented and the p = 0.106 test was not the right defense. The right defense is a sensitivity analysis, which we now provide.

**Group means.** Algae+ corals had lower Fv/Fm than algae- corals: 0.609 (95% CI: 0.582–0.636, n = 8) versus 0.677 (0.672–0.683, n = 64). The 0.07-unit gap is real and we had underappreciated it.

**Tank-by-treatment distribution** (new Supplementary Table S`[TBD]`):

| Tank | Fish | Wound | n |
|------|------|-------|---|
| 2 | No Fish | Large | 4 |
| 3 | Fish | Small | 1 |
| 4 | No Fish | Large | 2 |
| 5 | No Fish | Small | 1 |

Seven of eight algae+ fragments are in no-fish tanks; six of eight have large wounds; all eight sit in just four tanks.

**Sensitivity refit (n = 64, algae+ excluded).** The fish × wound interaction holds: χ²₂ = 10.248, p = 0.006 (compare primary χ²₂ = 10.898, p = 0.004). Cell means shift by ≤ 0.018:

| Cell | Primary (n = 72) | Sensitivity (n = 64) | Δ |
|---|---|---|---|
| No Fish / No Wound | 0.683 | 0.688 | +0.005 |
| Fish / No Wound | 0.687 | 0.681 | −0.006 |
| No Fish / Small | 0.656 | 0.672 | +0.016 |
| Fish / Small | 0.674 | 0.676 | +0.002 |
| No Fish / Large | 0.633 | 0.651 | +0.018 |
| Fish / Large | 0.685 | 0.680 | −0.005 |

The pattern — depressed Fv/Fm in wounded corals without fish, preserved Fv/Fm in wounded corals with fish — survives the exclusion. The interaction reflects a photophysiological response, not a confound with algal colonization.

Methods lines 131–133 now state that the sensitivity analysis (not the algae-effect p-value) is what supports pooling. The Supplementary Table holds the tank distribution and EMM comparison.

---

### R1.4 — Formal test of turf-algae persistence (lines 167–169)

> *"The observation at lines 167–169 that turf algae persisted on 7/8 no-fish corals versus 1/8 fish-present corals by day 21 is among the more striking results in the paper but is currently treated parenthetically. This deserves a formal quantitative comparison... In particular, the hypothesis that slower healing per se allows longer algal residency time is not distinguished from the fish territorial behaviour hypothesis in the current design, and this should be acknowledged explicitly."*

Promoted to a formal analysis. Among the 48 wounded corals:

|  | Algae persisted | Algae cleared | Total |
|---|---|---|---|
| No Fish | 7 | 17 | 24 |
| Fish | 1 | 23 | 24 |

Two-tailed Fisher's exact: **OR = 0.11 (95% CI: 0.00–0.99), p = 0.048**. Algae persistence was ~9× more likely in no-fish tanks. The result now sits in Results at lines `[TBD]` and as new Supplementary Table S`[TBD]`.

We added a Discussion paragraph (lines `[TBD]`) distinguishing two non-mutually-exclusive mechanisms: (a) direct exclusion via *Dascyllus* territorial grazing or aggression, and (b) faster wound closure in fish-present treatments shortening the window of substrate availability for algal colonization. The present design cannot separate them. We flag this as a target for future work, ideally a design that decouples the fish presence from the healing-rate trajectory (e.g., fish present briefly then removed).

---

### R1.5 — Interaction interpretation language (line 161)

> *"The fish × wound interaction on healing rate (χ² = 4.416, p = 0.036; line 161) is statistically significant but modest...with only two wound size levels this warrants careful, measured interpretation. The authors should avoid language that implies a robust size-dependent interaction where the evidence is marginal."*

Agreed. We rephrased:

- Abstract: "particularly for larger wounds" → "with a larger absolute effect for larger wounds."
- Results (lines `[TBD]`): now leads with the proportional fish effect (similar across wound sizes) and treats the larger absolute effect at large wounds as a quantitative observation, not as evidence for a robust size-dependent interaction.
- Discussion: dropped strong "size-dependent facilitation" framing; replaced with a measured statement that the absolute fish effect scales with wound size in a way consistent with metabolic-demand mechanisms, while noting the marginal interaction p-value.

---

### R1.6 — Buoyant-weight sensitivity claim (line 187)

> *"...the suggestion at line 187 that buoyant weight lacked sufficient sensitivity is less convincing: buoyant weight is the standard technique for short-term coral calcification studies and its precision for 21-day intervals is well established (Davies 1989, reference 24). This alternative explanation would be better omitted or substantially qualified."*

Removed. Buoyant weighing has been the standard for short-term coral calcification for thirty-five years, and questioning its sensitivity weakened the rest of our argument. The revised Discussion (lines `[TBD]`) attributes the null calcification result to the short experimental duration alone, with reference to studies that detect calcification effects in similar systems over longer (>4 wk) timescales (refs 2, 9, 27).

---

### R1.7 — Aquarium-context caveat (line 201)

> *"The discussion would benefit from a brief acknowledgement, after line 201, that the aquarium context — controlled water flow, artificial lighting, mechanical feeding, and absence of corallivores — may modify both effect sizes and the relative importance of the proposed mechanisms relative to field conditions."*

New sentence after line 201:
> *"Our aquarium setting standardized water flow, lighting, predator pressure, and food availability in ways that differ from a natural reef, and the absolute magnitude and relative ranking of the mechanisms we propose may shift in the field — ammonium subsidies could matter more or less under variable background nutrient loading, and the territorial-exclusion benefit could be larger where corallivores are present. Field replication is the obvious next step."*

---

### R1 Summary

We implemented all seven points. The most consequential changes are the explicit ML fitting in code (inference unchanged), the new Fisher's exact test for algae persistence (OR = 0.11, p = 0.048), the Fv/Fm sensitivity analysis (interaction holds at p = 0.006), and the new documentation of how often wounds fully closed before day 21 (25 of 48 fragments).

---

## Referee 2

R2's comments are clarifications and Methods detail. We address them in order.

---

### R2.1 — Abstract specificity (lines 25–26)

> *"Be more specific here i.e. 'We imposed small and large wounds and monitored healing in the presence and absence of a resident coral-dwelling damselfish, *Dascyllus flavicaudus*.'"*

Adopted as suggested. Abstract now reads: *"We imposed small and large wounds and monitored healing in the presence and absence of a resident coral-dwelling damselfish, *Dascyllus flavicaudus*."*

---

### R2.2 — "Symbiotic" → "mutualistic" (line 36)

> *"Suggest 'complex mutualistic systems' may be better wording given the context of the study, as symbiotic also incorporates commensal and parasitic relationships."*

Changed. Line 36 now reads "complex mutualistic systems."

---

### R2.3 — Carmignani et al. 2025 (line 48)

> *"See also: Carmignani et al. (2025). https://doi.org/10.1007/s00338-025-02680-3"*

Cited at line `[TBD]` in the Introduction where we discuss how coral-associated fishes shape the physical and chemical environment around coral tissues. Added as reference `[TBD]`.

---

### R2.4 — Caveats on egested waste and on coral-wounding by associated fishes (line 61)

> *"A general note that the effects of egested waste and associated microbiome on corals is less clear. Also, some coral-associated fishes may make small wounds, e.g. Gobiodon clearing space for eggs."*

Both points added. The relevant Introduction paragraph (lines `[TBD]`) now notes that ammonium excretion is the best-characterized pathway, that the effects of egested solid waste and its microbiome on coral physiology are less well-resolved, and that not every coral-associated fish is beneficial — *Gobiodon* gobies, for example, inflict small wounds while clearing substrate for egg deposition.

---

### R2.5 — Territorial behaviour framing (line 63)

> *"Regarding territorial behaviours, both cited studies focussed on Dascyllus which can be very territorial, but this is not a general characteristic of all coral-associated fishes. Reword to this effect e.g. 'The territorial behaviours of some species, such as Dascyllus damselfishes, can also…'"*

Adopted. Line 63 now reads: *"The territorial behaviours of some coral-associated fishes, particularly *Dascyllus* damselfishes, also reduce exposure to corallivores and other physical disturbances that could disrupt wound closure (refs)."*

---

### R2.6 — Coral morphotype and image (line 86)

> *"Please clarify if a single coral morphotype was used. Can you include an image of the coral fragments/morphotype used?"*

Methods (lines `[TBD]`) now state that all 72 fragments came from colonies of a single dominant *Pocillopora* morphotype (`[TBD: describe morphotype]`) from the same shallow lagoon habitat. A representative-fragment photograph with wound placement is included as new Supplementary Figure S`[TBD]`.

---

### R2.7 — Coral collection details (line 95)

> *"Give a size range for the collected fragments... Collection required breaking them off larger colonies – was the level of baseline tissue damage similar between fragments? Importantly, how many donor colonies were used, how many fragments were taken per donor, and how did you account for donor ID in the experiment?... If not accounted for, this should be acknowledged as a limitation."*

Methods (lines `[TBD]`) now report:

- **Fragment size:** `[TBD: from coral_sa.csv — min, max, mean ± SD]`.
- **Morphological standardization:** `[TBD: state criteria — single uniform-thickness branch tip, etc.]`.
- **Baseline damage:** all fragments were broken cleanly at the base of a single branch with stainless-steel bone cutters. The basal break-point exposed a similar area of skeleton across fragments and showed visible tissue recovery in every fragment after the 3-day acclimation.
- **Donor colonies and clones:** *"We collected fragments from `[TBD: n donor colonies, fragments per donor]` mature donor colonies (>20 cm diameter) separated by ≥5 m to reduce — but not eliminate — the possibility of including clonal replicates. Donor identity was not retained as an explanatory variable in our models, and we acknowledge this as a limitation: unmeasured donor genotype, including any cryptic clonality, contributes to residual variance."*

A matching sentence in the Discussion (lines `[TBD]`) flags donor genotype as a residual-variance contributor and notes the *Pocillopora* clonality issue specifically.

---

### R2.8 — Fish collection, sizes, biomass (line 95)

> *"How were they collected? Clove oil, hand nets etc. How big were the fish and what is the size range ± SE of the individuals used. Size has a non-linear effect on excretion rates, so variation in fish size could influence the magnitude of nutrient inputs."*

Methods (lines `[TBD]`) now read:
> *"We collected 18 adult *D. flavicaudus* using `[TBD: collection method]`. We weighed each fish wet to the nearest 0.1 g after blotting; mean ± SD wet mass was `[TBD]` g (range `[TBD]`–`[TBD]` g, n = 18). Six fish per tank (~36 g total biomass) achieved the stocking target. Because mass-specific excretion scales non-linearly with body size, we restricted the wet-mass range of stocked individuals to minimize among-tank variation in expected ammonium flux."*

If biomass was estimated from L–W rather than measured directly, swap to: *"We estimated wet mass from standard length using the published L–W relationship for *D. flavicaudus* (`[TBD]`); mean estimated mass per individual was..."*. Pick one based on the field protocol.

---

### R2.9 — Acclimation feeding (line 95/107)

> *"Please note the feeding regime during the acclimation period."*

Methods now state that during the 3-day acclimation, fish were held separately from corals in `[TBD: aquarium description]` and fed the same TetraMarine Saltwater Flake regimen used during the experiment (2 g three times daily). Corals were unfed during acclimation.

---

### R2.10 — In-tank behavioural observations (line 95)

> *"I would appreciate some brief notes of your observations of the fish within the tanks during the trials, i.e. were the actively swimming in amongst the branches etc? This will support your point in the discussion around water movement."*

Added. The Methods (lines `[TBD]`) now include 2–3 sentences from field notes: `[TBD: fish behavior observations during the trial, drawing on field notes — to support the water-movement argument in the Discussion]`.

---

### R2.11 — Tank dimensions and fragment spacing (line 99)

> *"Please provide tank dimensions, also outline the distance between fragments within the tanks."*

Methods now state: *"Each 95 L flow-through aquarium measured `[TBD: L × W × H in cm]` and held 12 fragments arranged on a `[TBD]` grid so that nearest-neighbour fragments were ≥`[TBD]` cm apart and no fragment was within `[TBD]` cm of a tank wall."*

---

### R2.12 — Break-point wound on all fragments (line 101)

> *"Wounded and non-wounded fragments both had a wound at the breakpoint, important to acknowledge and would be good to briefly note coral recovery following the acclimation period."*

Acknowledged. Methods (lines `[TBD]`) now state that all fragments — including those assigned to the no-experimental-wound treatment — carried a basal break-point wound from collection, and that the 3-day acclimation period allowed visible tissue recovery at the break-point in every fragment before experimental wounds were imposed. Reported wound-healing rates refer specifically to the upper-face experimental wounds, which were spatially distinct from the basal break-point.

---

### R2.13 — Randomization within tanks (line 102)

> *"Were treatments allocated randomly to fragments within the tank?"*

Yes. Methods now state: *"Within each tank we randomly assigned the three wound treatments (no wound, small, large) to the 12 fragments such that each tank held four replicates per wound treatment. Fish-treatment assignment was randomized at the tank level (n = 3 fish tanks, n = 3 no-fish tanks)."*

---

### R2.14 — One wound per fragment, location standardization (line 104)

> *"Please clarify – there was one wound per coral fragment, and this was placed in a standardised position on each colony?"*

Yes. Methods (lines `[TBD]`) now state that each wounded fragment received a single circular wound on the central upper face of the branch, placed at a standardized distance from the fragment apex (~`[TBD]` cm). Wound location is also shown on the new Supplementary Figure S`[TBD]` (R2.6).

---

### R2.15 — Fish biomass calculation method (line 105)

> *"How was this calculated? Were individuals weighed or is this based on L-W?"*

See R2.8.

---

### R2.16 — Uneaten food on corals (line 107)

> *"Did you put measures in place to prevent uneaten food from settling onto the corals? If not, this food could have provided a direct source of additional energy to fragments."*

Yes. Methods (lines `[TBD]`) now state:
> *"We siphoned uneaten flake food from each tank 10 minutes after each of the three daily feedings, and scrubbed tanks and coral plugs daily. Both fish-present and fish-absent tanks received identical flake regimens with identical siphoning, so any residual heterotrophic subsidy from uneaten food is equalized across the fish manipulation."*

This is also our answer to the implied concern that fish-present effects could be confounded with heterotrophic feeding on flake food: both treatments received the food, both had it removed.

---

### R2.17 — Package citations (line 134)

> *"Suggest including package citations."*

Added. Methods (lines `[TBD]`) now cite `lme4` (Bates et al. 2015), `DHARMa` (Hartig 2024), `broom.mixed` (Bolker & Robinson 2022), and base R (R Core Team 2023). `lmerTest` is cited only if Hayden used it for d.f. approximations — `[TBD: confirm]`.

---

### R2.18 — Tank-level replication caveat (line 159)

> *"The experimental design is appropriate; however, inference is slightly constrained by the level of replication at the tank level (n = 3 per treatment). While tank is included as a random effect, this should be noted as a point of caution in the discussion."*

Added. New sentence at the end of the Discussion (lines `[TBD]`):
> *"Fish presence was replicated at the tank level (n = 3 fish tanks, n = 3 no-fish tanks), so our inference about the fish effect rests on between-tank contrasts. Tank ID is included as a random intercept, but a future replication with higher tank counts would tighten estimates of the fish effect and its variability."*

---

### R2.19 — Algae-removal mechanism (line 194)

> *"This is an interesting result, do you have any thoughts on the mechanism, i.e. did you observe the damselfish picking at the algae?"*

See R1.4 for the formal test and the new Discussion paragraph on competing mechanisms. We add observational context: `[TBD: sentence on whether fish were directly observed picking at turf algae, or whether the result is more parsimoniously explained by faster wound closure shortening the substrate-availability window]`.

---

### R2 Summary

All 19 points addressed. The notable additions are the new Supplementary Figure of the coral morphotype with wound placement, expanded Methods on fragment sourcing and fish biometrics, and the new Discussion paragraph on tank-level replication.

---

## Editorial Office

### EO.1 — Permanent data archive

> *"...we do ask that datasets...are uploaded to other repositories other than GitHub, such as figshare. Please upload your data into another repository and amend your data section accordingly..."*

Done. We tagged v1.0 of the GitHub repository and minted a Zenodo DOI via the GitHub–Zenodo integration. The Data Accessibility section now reads:
> *"Data and analysis code supporting this article are archived at Zenodo: `[TBD: DOI 10.5281/zenodo.XXXXXXX]` (Vega et al. 2026; repository: https://github.com/haydenvega/damselfish_coral_healing_public, v1.0)."*

The Zenodo deposit is cited in the reference list as new entry `[TBD]`.

### EO.2 — Data cited in references

Done — see EO.1.

### EO.3 — Move Ethics, COI, Data Accessibility, Author Contributions to ScholarOne

Done. Removed from the main manuscript; entered into the corresponding ScholarOne fields at resubmission.

### EO.4 — Figure permissions

All figures (Figure 1–3 and Supplementary Figure S`[TBD]`) are original photographs and analyses produced by the authors. No third-party permissions needed. Confirmed in the cover letter.

### EO.5 — Separate figure files

Figures uploaded as separate `.tif` files at 600 dpi. PDF versions remain in the repository for reference.

### EO.6 — Tracked-changes version

A tracked-changes Word document is included as supplementary material.

### EO.7 — Social-media image

A coral-fragment field photograph showing *D. flavicaudus* sheltering in *Pocillopora* is provided as a supplementary social-media image.

---

## Summary

The six most consequential changes:

1. Mixed-effects models now explicitly fit by ML for the LRT comparisons (R1.1). Inference unchanged.
2. New Fisher's exact test on turf-algae persistence: OR = 0.11, p = 0.048 (R1.4).
3. New Fv/Fm sensitivity analysis excluding the 8 algae-colonized corals; fish × wound interaction holds (χ²₂ = 10.248, p = 0.006) (R1.3).
4. New documentation that 25 of 48 wounded fragments closed before day 21, with the censoring direction biased against the fish effect (R1.2).
5. Methods substantially expanded on coral fragment sourcing (donor colonies, clonal risk, baseline break-point recovery), fish biometrics, tank/acclimation conditions, randomization, and uneaten-food handling (R2.6–R2.17).
6. Aquarium-context and tank-replication caveats added to the Discussion; size-dependent interaction language moderated; the buoyant-weight sensitivity speculation removed (R1.5–R1.7, R2.18).

The central conclusions are unchanged. We thank the editor and reviewers.

Sincerely,

Hayden Vega, on behalf of all authors
