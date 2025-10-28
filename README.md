# Damselfish‑Coral Healing Project
Repository for the publication: *Coral‑Associated Fishes Accelerate Coral Wound Healing and Photosynthetic Recovery*

## Table of Contents
- [General Information](#general-information)  
  - [1. Authors](#1-authors)  
  - [2. Dates of data collection](#2-dates-of-data-collection)  
  - [3. Location of data collection](#3-location-of-data-collection)  
  - [4. Funding Sources](#4-funding-sources)  
- [Sharing / Access Information](#sharing--access-information)  
  - [1. Licenses / restrictions placed on the data](#1-licenses--restrictions-placed-on-the-data)  
  - [2. Links to publications that cite or use the data](#2-links-to-publications-that-cite-or-use-the-data)  
  - [3. Links to other publicly accessible locations of the data](#3-links-to-other-publicly-accessible-locations-of-the-data)  
  - [4. Links / relationships to ancillary datasets](#4-links--relationships-to-ancillary-datasets)  
  - [5. Data derivation](#5-data-derivation)  
  - [6. Recommended citation for this dataset](#6-recommended-citation-for-this-dataset)  
- [Data and File Overview](#data-and-file-overview)  
  - [1. File list](#1-file-list)  
  - [2. Relationship between files](#2-relationship-between-files)  
  - [3. Data versions](#3-data-versions)  
- [Methodological Information](#methodological-information)  
  - [1. Study goals](#1-study-goals)  
  - [2. Description of methods](#2-description-of-methods)   
  - [3. Description of quality-assurance procedures performed on the data](#4-description-of-quality-assurance-procedures-performed-on-the-data)  
- [Variable Descriptions (Data Dictionary)](#variable-descriptions-data-dictionary)  
- [Citations](#citations)

---

## General Information

### 1. Authors
- Hayden Vega, University of California Santa Barbara, haydenvega@ucsb.edu  
- Adrian Stier, University of California Santa Barbara, astier@ucsb.edu

### 2. Dates of data collection
2024-06-27 to 2024-09-06

### 3. Location of data collection
Specimens were collected in Mo’orea, French Polynesia (Moorea Coastal Research Long‑Term Ecological Research site: MRB). Laboratory measurements were conducted at Gump Field Station.

### 4. Funding Sources
Supported by the Keck Foundation and the National Science Foundation (OCE-1851510 and OCE-1851032). This work was also facilitated by resources provided by the NSF-funded Moorea Coral Reef Long-term Ecological Research program funded by OCE-1637396 and previous awards. Student funding came from the UCSB Worster Fellowship.

---

## Sharing / Access Information

### 1. Licenses / restrictions placed on the data
Data are shared under the Creative Commons Attribution 4.0 International (CC BY 4.0): https://creativecommons.org/licenses/by/4.0/.

### 2. Links to publications that cite or use the data
Vega, H. & Stier, A. (2025). *Coral‑Associated Fishes Accelerate Coral Wound Healing and Photosynthetic Recovery*. [Journal reference pending].

### 3. Links to other publicly accessible locations of the data
N/A

### 4. Links / relationships to ancillary datasets
N/A

### 5. Data derivation
The dataset is primary experimental data generated as part of this project, not derived from secondary sources.

### 6. Recommended citation for this dataset
Vega, H. & Stier, A. 2025. Damselfish–Coral Healing Experimental Dataset. coral wound healing & photosynthetic recovery experiment. Repository: https://github.com/haydenvega/damselfish_coral_healing_public.

---

## Data and File Overview

### 1. File list
```
├── data/
│   ├── Copy of fish_regen_mastersheet_wound closure_necrosis - mastersheet.csv
│   ├── coral_delta.csv
│   ├── coral_sa.csv
│   ├── final_wound_size_dascyllus_project - Sheet1.csv
│   ├── fish_regen_buoyantweight (1).csv
│   ├── fish_regen_mastersheet_wound closure_necrosis_sa - mastersheet.csv
│   ├── pam_healed.csv
│   ├── pam_undisturbed_healed.csv
│   ├── pam_undisturbed_healed_tissue_wound_no_wound.csv
│   ├── skeletal.xlsx
│   ├── wax_dip_calibrations.csv
│   └── wax_dip_corals.csv
├── analysis_visualization_code/
│   ├── growth/
│   │   ├── allometric_growth_analysis.Rmd
│   │   └── SA_calibration_calculations_5_13.R
│   ├── photo_eff/
│   │   └── pam_analysis.Rmd
│   └── wound/
│       └── wound_closure_analysis.Rmd
├── figures/
│   └── (output figures – e.g., initial_mass_by_treatment.png, scaled_growth_by_treatment.png)
├── damselfish_coral_healing_public.Rproj
├── README.md
└── LICENSE
```

### 2. Relationship between files
- `data/` contains cleaned input datasets: buoyant weight, surface area, wound healing, and metadata.  
- `analysis_visualization_code/` contains scripts and R Markdown for generating figures and analyses.  
- `figures/` contains final high‑resolution graphics for publication.  
- The R project file (`.Rproj`) encapsulates the analysis environment.

### 3. Data versions
This is the first publicly released version of the dataset (Version 1.0).

---

## Methodological Information

### 1. Study goals
The study aimed to evaluate how the presence of damselfish and the size of induced wounds influence tissue regeneration, volume/buoyant weight increase, and photosynthetic recovery in coral fragments of Pocillopora spp.

### 2. Description of methods

#### Study site and system
August 2024, Richard B. Gump South Pacific Research Station, Mo’orea, French Polynesia (17°30′S, 149°50′W). Experiment tested effects of yellowtail damselfish (Dascyllus flavicaudus) on wound regeneration and photosynthetic recovery in Pocillopora spp. Summary statistics reported as mean ± SD.

#### Collection and experimental setup
72 Pocillopora fragments (from mature colonies >20 cm) and 18 adult D. flavicaudus were collected from a northshore lagoon reef and transported to Gump Field Station. Fragments mounted on ceramic plugs and randomly distributed across six 95 L flow‑through tanks (12 fragments/tank; flow ≈ 6 L h−1). After 3 days acclimation, fragments were assigned to control (no wound), small wound (1.48 ± 0.40 cm2), or large wound (3.82 ± 1.08 cm2); 4 fragments per treatment per tank. Six fish (≈36 g total biomass) were added to half the tanks (n = 3); remaining tanks were fishless controls. All tanks fed 2 g TetraMarine flakes three times daily; uneaten food removed after 10 min.

#### Measurements and endpoints
- Wound healing: photographs (Olympus TG‑6) immediately and on day 21; areas measured in ImageJ; wound scored healed/unhealed. Healing rate = (initial_area − final_area)/21 (cm2 day−1).  
- Growth: buoyant weight measured day 1 and day 21 (Davies 1989); surface area via wax‑dip calibration; growth rate = (final_weight − initial_weight)/(surface_area × 21) (mg cm−2 day−1).  
- Photosynthesis: dark‑adapted Fv/Fm measured day 21 with Diving‑PAM (Walz); measurement location: upper face for controls, adjacent to wound for wounded fragments. Algae near wounds removed in 8 fragments; effect of algae on Fv/Fm non‑significant (p = 0.106).

#### Data processing and analysis
Data cleaned in R (janitor::clean_names()); derived variables computed (delta mass, growth rates, log transforms). Mixed‑effects models fitted with lme4::lmer() using tank as a random intercept; likelihood‑ratio tests used for model comparison. All raw data, cleaning scripts, cleaned outputs, and analysis Rmds are included in the repository.

#### Ethics and permits
Field collection and experiments conducted under relevant permits and institutional approvals [insert permit numbers and issuing authorities].


### 3. Description of quality‑assurance procedures performed on the data
Raw data were double‑checked for entry errors. Missing or damaged fragments are coded as `NA`. The experimental design was verified for initial size equivalence across treatments.

## Variable Descriptions (Data Dictionary)

### final_wound_size_dascyllus_project - Sheet1.csv

| Variable | Description |
|---|---|
| `coral_id` | Unique identifier for each coral fragment |
| `date_collected` | Date the coral fragment was collected |
| `date_fragment` | Date the coral was fragmented |
| `fish` | Presence of fish (`1` = fish present, `0` = no fish) |
| `wound` | Wound treatment group (`1` = small wound, `2` = large wound) |
| `tank` | Tank number where the coral was housed |
| `wound_size_final` | Final wound size in centimeters |
| `percent healed` | Percentage of wound healed over the experiment duration |
| `initial_wound_size_cm` | Initial wound size in centimeters |
| `healing_rate` | Rate of healing per day (cm/day) |
| `time_healing_days` | Duration of healing period in days |

---

### fish_regen_buoyantweight (1).csv

| Variable | Description |
|---|---|
| `date` | Measurement time point (`initial` or `final`) |
| `coral_id` | Unique identifier for each coral fragment |
| `bouyantweight_g` | Coral buoyant weight in grams |
| `air_temp_c` | Air temperature during weighing (°C) |
| `air_weight_g` | Coral weight in air (grams) |
| `fresh_temp_c` | Temperature of fresh water during weighing (°C) |
| `fresh_weight_g` | Coral weight in fresh water (grams) |
| `salt_temp_c` | Temperature of salt water during weighing (°C) |
| `salt_weight_g` | Coral weight in salt water (grams) |
| `density_aragonite` | Density of aragonite used for buoyant weight calculations (g/cm³) |
| `wound` | Wound treatment group (`Small`, `Large`, or `No Wound`) |
| `fish` | Fish treatment group (`Fish` or `No Fish`) |

---

### pam_healed.csv

| Variable | Description |
|---|---|
| `coral_id` | Unique identifier for each coral fragment |
| `f0` | Initial fluorescence reading (Fo) |
| `fm` | Maximum fluorescence reading (Fm) |
| `fv_fm` | Photosynthetic efficiency (Fv/Fm ratio) |
| `wound` | Wound treatment group (`Small` or `Large`) |
| `fish` | Fish treatment group (`Fish` or `No Fish`) |
| `tank` | Tank number where the coral was housed |
| `initial_wound_size` | Initial wound size in centimeters |
| `algae` | Presence of algae (`yes` or `no`) |

---

## Citations
Vega, H. & Stier, A. (2025). *Coral‑Associated Fishes Accelerate Coral Wound Healing and Photosynthetic Recovery*. [Journal reference pending].
