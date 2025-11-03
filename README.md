![Damselfish and Coral](images/DAFL-photo.jpeg)

# Damselfish-Coral Healing: Experimental Dataset & Analysis Code

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![DOI](https://img.shields.io/badge/DOI-pending-blue.svg)](#)
[![R Version](https://img.shields.io/badge/R-%E2%89%A54.5.0-blue.svg)](https://www.r-project.org/)

**Supporting:** Vega, H. & Stier, A. (2025). *Coral-Associated Fishes Accelerate Coral Wound Healing and Photosynthetic Recovery*. [Journal pending].

**Authors:** Hayden Vega (haydenvega@ucsb.edu) & Adrian Stier (astier@ucsb.edu)
**Institution:** University of California Santa Barbara
**Version:** 1.0
**Last Updated:** October 2024

---

## Table of Contents

- [Overview](#overview)
- [Repository Structure](#repository-structure)
- [Installation & Requirements](#installation--requirements)
- [Quick Start](#quick-start)
- [Data Documentation](#data-documentation)
- [Analysis Workflow](#analysis-workflow)
- [Key Findings](#key-findings)
- [Citation](#citation)
- [Funding & Acknowledgments](#funding--acknowledgments)
- [License](#license)
- [Contact](#contact)

---

## Overview

This repository contains all data, analysis code, and documentation for an experimental study investigating how coral-associated damselfish (*Dascyllus flavicaudus*) influence wound healing and photosynthetic recovery in branching corals (*Pocillopora* spp.).

### Research Questions

1. **Do damselfish accelerate coral wound healing?**
2. **How does wound size affect coral skeletal growth rates?**
3. **Does fish presence buffer coral photosynthetic stress from wounding?**

### Experimental Design

- **Location:** Mo'orea, French Polynesia (Gump Research Station)
- **Duration:** 21-day mesocosm experiment (August 2024)
- **Design:** 2 × 3 factorial (Fish Presence × Wound Size)
  - **Fish:** Present vs. Absent (6 *D. flavicaudus* per tank)
  - **Wound:** No Wound, Small (~1.5 cm²), Large (~3.8 cm²)
- **Replication:** 72 coral fragments across 12 flow-through tanks
- **Response Variables:**
  - Wound healing rate (cm²/day)
  - Size-corrected skeletal growth (allometric scaling)
  - Photosynthetic efficiency (Fv/Fm)

---

## Repository Structure

```
damselfish_coral_healing_public/
│
├── data/                              # All experimental datasets
│   ├── DATA_METADATA.txt              # Comprehensive data documentation
│   ├── *_METADATA.txt                 # Individual metadata files for each dataset
│   ├── fish_regen_buoyantweight (1).csv   # Skeletal mass measurements
│   ├── final_wound_size_dascyllus_project - Sheet1.csv  # Wound healing data
│   ├── pam_undisturbed_healed_tissue_wound_no_wound.csv  # PAM fluorometry
│   ├── fish_regen_mastersheet_wound closure_necrosis_sa - mastersheet.csv  # Metadata
│   ├── wax_dip_*.csv                  # Surface area measurements
│   └── ... [see Data Documentation section]
│
├── analysis_visualization_code/      # Analysis scripts
│   ├── wound/
│   │   └── wound_closure_analysis.Rmd      # Wound healing analysis
│   ├── growth/
│   │   ├── allometric_growth_analysis.Rmd  # Skeletal growth analysis
│   │   └── SA_calibration_calculations_5_13.R  # Surface area calibration
│   └── photo_eff/
│       └── pam_analysis.Rmd                # PAM fluorometry analysis
│
├── figures/                           # Publication-quality figures
│   ├── wound_closure/                 # Healing rate figures (PDF + PNG)
│   ├── growth/                        # Growth rate figures (PDF + PNG)
│   ├── pam/                           # Photosynthetic efficiency figures
│   └── diagnostics/                   # Model diagnostic plots
│
├── images/                            # Repository images
│   └── DAFL-photo.jpeg                # Damselfish image
│
├── damselfish_coral_healing_public.Rproj  # RStudio project file
├── README.md                          # This file
└── LICENSE                            # CC BY 4.0 license

```

---

## Installation & Requirements

### Software Requirements

- **R:** Version ≥ 4.5.0
- **RStudio:** Recommended for running `.Rmd` files

### R Package Dependencies

```r
# Data manipulation
install.packages(c("tidyverse", "janitor", "here"))

# Statistical modeling
install.packages(c("lme4", "DHARMa", "MuMIn", "parameters", "broom.mixed"))

# Visualization
install.packages(c("ggplot2", "viridis", "ggeffects", "ggpubr", "gt"))

# Additional
install.packages(c("readxl", "effects", "sjlabelled"))
```

### Installation

```bash
# Clone repository
git clone https://github.com/haydenvega/damselfish_coral_healing_public.git
cd damselfish_coral_healing_public

# Open RStudio project
open damselfish_coral_healing_public.Rproj
```

---

## Quick Start

### Run Complete Analysis Pipeline

1. **Open RStudio project:**
   ```r
   # Double-click damselfish_coral_healing_public.Rproj
   ```

2. **Run analyses in order:**

   ```r
   # 1. Surface area calibration
   source("analysis_visualization_code/growth/SA_calibration_calculations_5_13.R")

   # 2. Wound healing analysis
   rmarkdown::render("analysis_visualization_code/wound/wound_closure_analysis.Rmd")

   # 3. Allometric growth analysis
   rmarkdown::render("analysis_visualization_code/growth/allometric_growth_analysis.Rmd")

   # 4. PAM fluorometry analysis
   rmarkdown::render("analysis_visualization_code/photo_eff/pam_analysis.Rmd")
   ```

3. **View HTML reports:**
   - `wound_closure_analysis.html`
   - `allometric_growth_analysis.html`
   - `pam_analysis.html`

### Expected Runtime

- Surface area calibration: ~30 seconds
- Each analysis: ~2-5 minutes
- Total pipeline: ~10-15 minutes

---

## Data Documentation

### Primary Datasets

| File | Description | Observations | Used In |
|------|-------------|--------------|---------|
| `fish_regen_buoyantweight (1).csv` | Buoyant weight measurements (initial & final) | 144 | Growth analysis |
| `final_wound_size_dascyllus_project - Sheet1.csv` | Wound healing measurements | 48 | Wound analysis |
| `pam_undisturbed_healed_tissue_wound_no_wound.csv` | PAM fluorometry (Fv/Fm) | 72 | PAM analysis |
| `fish_regen_mastersheet_..._sa - mastersheet.csv` | Treatment assignments + surface area | 72 | All analyses |

### Metadata Files

Each dataset has a corresponding `*_METADATA.txt` file containing:
- Variable descriptions and units
- Measurement protocols
- Quality control procedures
- Statistical analysis details
- Usage guidelines

**Primary metadata files:**
- `DATA_METADATA.txt` - Comprehensive overview of all datasets
- `fish_regen_buoyantweight_(1)_METADATA.txt` - Skeletal mass data
- `final_wound_size_dascyllus_project_METADATA.txt` - Wound healing data
- `pam_fluorometry_METADATA.txt` - PAM data (3 files)
- `wax_dip_surface_area_METADATA.txt` - Surface area methods
- `mastersheet_METADATA.txt` - Treatment assignments

### Data Dictionary Quick Reference

#### Treatment Coding

```r
# Fish presence
0 = "No Fish"  (control tanks)
1 = "Fish"     (6 damselfish per tank)

# Wound size
0 = "No Wound" (unwounded control)
1 = "Small"    (~1.5 cm² wound)
2 = "Large"    (~3.8 cm² wound)

# Tank: 1-12 (used as random effect in all models)
```

#### Key Response Variables

- **Healing rate:** (initial_wound_size - final_wound_size) / 21 days (cm²/day)
- **Growth rate:** (final_mass - initial_mass) / (surface_area × 21) (mg/cm²/day)
- **Allometric growth:** log(final_mass / initial_mass^b) where b = scaling coefficient
- **Fv/Fm:** (Fm - F0) / Fm, photosystem II quantum efficiency (0-1 scale)

---

## Analysis Workflow

### 1. Surface Area Calibration

**Script:** `SA_calibration_calculations_5_13.R`

**Purpose:** Generate calibration curve to convert wax coating mass to coral surface area

**Inputs:**
- `wax_dip_calibrations.csv` (geometric standards)
- `wax_dip_corals.csv` (coral measurements)

**Outputs:**
- `coral_sa.csv` (calibrated surface areas)
- Calibration curve diagnostics

**Method:** Linear regression of wax mass vs. known surface area

---

### 2. Wound Healing Analysis

**Script:** `wound_closure_analysis.Rmd`

**Key Analyses:**
- Daily healing rates by fish and wound size
- Proportion healed (beta regression)
- Mixed-effects models with tank as random effect
- DHARMa diagnostics

**Statistical Models:**
```r
# Primary model
healing_rate ~ fish * wound + (1 | tank)

# Beta regression for proportions
prop_healed ~ fish * wound + (1 | tank), family = beta()
```

**Figures Generated:**
- Mean healing rates with error bars (PDF + PNG)
- DHARMa diagnostic plots
- Residual diagnostics

---

### 3. Allometric Growth Analysis

**Script:** `allometric_growth_analysis.Rmd`

**Key Analyses:**
- Allometric scaling coefficient estimation
- Size-corrected growth rates
- Surface area-normalized growth
- Mixed-effects models

**Statistical Models:**
```r
# Allometric scaling
log(final_mass) ~ log(initial_mass) + wound

# Size-corrected growth
allometric_growth ~ fish * wound + (1 | tank)

# Growth rate per unit area
growth_rate_per_cm2 ~ fish * wound + (1 | tank)
```

**Figures Generated:**
- Allometric scaling relationship
- Mean growth rates by treatment (PDF + PNG)
- Model diagnostics

---

### 4. PAM Fluorometry Analysis

**Script:** `pam_analysis.Rmd`

**Key Analyses:**
- Photosynthetic efficiency (Fv/Fm) by treatment
- Effects of fish and wound on photosynthetic health
- Algae colonization effects (tested, non-significant)
- Mixed-effects models

**Statistical Models:**
```r
# Primary model
fv_fm ~ fish * wound + (1 | tank)

# Algae effect (subset analysis)
fv_fm ~ fish * wound + algae + (1 | tank)
```

**Figures Generated:**
- Mean Fv/Fm by treatment with error bars (PDF + PNG)
- Model diagnostics

---

### Statistical Approach (All Analyses)

**Model Structure:**
- Linear mixed-effects models (`lme4::lmer`)
- Fixed effects: Fish (2 levels) × Wound (2-3 levels)
- Random effect: Tank (12 tanks) as random intercept
- Hypothesis testing: Likelihood ratio tests (LRT)
- Diagnostics: DHARMa simulated residuals (n=1000)

**Factor Level Ordering:**
- Fish: "No Fish" → "Fish"
- Wound: "No Wound" → "Small" → "Large"

**Model Validation:**
- QQ plots for normality
- Residual vs. fitted for homoscedasticity
- DHARMa tests for dispersion and outliers
- Predicted vs. observed plots

---

## Key Findings

### 1. Wound Healing

- **Fish presence significantly accelerates wound healing**
- Small wounds heal faster than large wounds
- Many small wounds achieved 100% closure by Day 21
- Fish effect stronger for large wounds (interaction trend)

### 2. Skeletal Growth

- **Wound size reduces growth rates** (more severe for large wounds)
- Fish presence shows positive growth effects
- Allometric scaling coefficient (b) ≈ 0.7-0.9 for *Pocillopora*
- Growth rates: ~X mg/cm²/day [values from analysis]

### 3. Photosynthetic Efficiency

- **Fish presence enhances photosynthetic efficiency (Fv/Fm)**
- Wound size shows measurable stress effects
- Fish appears to buffer wound stress
- No significant fish × wound interaction
- Algal colonization not a significant confound (p = 0.106)

### Ecological Implications

Coral-associated damselfish provide multiple benefits to host corals:
1. Enhanced tissue regeneration
2. Maintained photosynthetic function under stress
3. Potential mechanisms: nutrient provisioning (ammonium), protection from competitors

---

## Citation

### Dataset Citation

```
Vega, H. & Stier, A. (2025). Damselfish-Coral Healing Experimental Dataset.
Repository: https://github.com/haydenvega/damselfish_coral_healing_public
DOI: [pending]
```

### Publication Citation

```
Vega, H. & Stier, A. (2025). Coral-Associated Fishes Accelerate Coral Wound
Healing and Photosynthetic Recovery. [Journal reference pending].
```

### BibTeX

```bibtex
@misc{vega2025damselfish_data,
  author = {Vega, Hayden and Stier, Adrian},
  title = {Damselfish-Coral Healing Experimental Dataset},
  year = {2025},
  publisher = {GitHub},
  url = {https://github.com/haydenvega/damselfish_coral_healing_public},
  doi = {pending}
}

@article{vega2025damselfish,
  author = {Vega, Hayden and Stier, Adrian},
  title = {Coral-Associated Fishes Accelerate Coral Wound Healing and Photosynthetic Recovery},
  journal = {[Journal pending]},
  year = {2025},
  doi = {pending}
}
```

---

## Funding & Acknowledgments

### Funding Sources

- **W.M. Keck Foundation**
- **National Science Foundation:**
  - OCE-1851510
  - OCE-1851032
  - OCE-1637396 (Moorea Coral Reef LTER)
- **UCSB Worster Fellowship** (student funding)

### Acknowledgments

This work was facilitated by the NSF-funded Moorea Coral Reef Long-Term Ecological Research (MCR-LTER) program. We thank the staff at Richard B. Gump South Pacific Research Station for logistical support and the UC Natural Reserve System for access to research facilities.

### Field Permits

Field collection and experiments conducted under permits issued by the French Polynesian government [permit numbers pending].

---

## License

This dataset is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** license.

**You are free to:**
- Share — copy and redistribute the material
- Adapt — remix, transform, and build upon the material

**Under the following terms:**
- **Attribution** — You must give appropriate credit, provide a link to the license, and indicate if changes were made

Full license: https://creativecommons.org/licenses/by/4.0/

---

## Contact

### Authors

**Hayden Vega**
PhD Student, Department of Ecology, Evolution, and Marine Biology
University of California Santa Barbara
Email: haydenvega@ucsb.edu

**Adrian Stier**
Associate Professor, Department of Ecology, Evolution, and Marine Biology
University of California Santa Barbara
Email: astier@ucsb.edu
Lab Website: [Stier Lab](https://www.thestierlab.com/)

### Issues & Questions

- **Data questions:** Contact Hayden Vega (haydenvega@ucsb.edu)
- **Code issues:** Open an issue on GitHub
- **Collaboration inquiries:** Contact Adrian Stier (astier@ucsb.edu)

---

## Additional Resources

### Related Publications

[To be added upon publication]

### Data Repositories

- **GitHub:** https://github.com/haydenvega/damselfish_coral_healing_public
- **Zenodo:** [DOI pending]
- **MCR-LTER Data:** [link pending]

### Methods References

- **Buoyant weighing:** Davies, P.S. (1989). Short-term growth measurements of corals using an accurate buoyant weighing technique. *Marine Biology* 101:389-395.
- **PAM fluorometry:** Maxwell, K. & Johnson, G.N. (2000). Chlorophyll fluorescence—a practical guide. *Journal of Experimental Botany* 51:659-668.
- **Surface area:** Veal, C.J. et al. (2010). Coral surface area quantification. *Coral Reefs* 29:93-97.

---

**Last Updated:** October 28, 2024
**Repository Version:** 1.0
**Status:** Publication pending

---

<div align="center">

**If you use this dataset, please cite both the data repository and the associated publication.**

[![GitHub](https://img.shields.io/badge/GitHub-Repository-black?logo=github)](https://github.com/haydenvega/damselfish_coral_healing_public)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

</div>
