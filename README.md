# PFAS Contamination and Racial Disparities in New Jersey

## Project Overview

This project investigates whether PFAS (per- and polyfluoroalkyl substances) contamination in New Jersey drinking water is disproportionately concentrated in communities of color, lower-income neighborhoods, and areas near industrial facilities. Using data from the EPA's Unregulated Contaminant Monitoring Rule (UCMR 5), ZIP code-level and water-system-level demographic data from the U.S. Census, Zillow home value data, EPA ECHO industrial facility data, and EPA public water system service area boundaries, the analysis examines PFAS exposure across NJ at two geographic scales: ZIP codes and water system service areas.

---

## Directory Structure

```
QSS20-CW-Final/
├── code/               # Jupyter notebooks (run in order: 00 → 04)
├── data/
│   ├── raw/            # ⚠️ Large raw files — NOT on GitHub, download separately (see below)
│   ├── 01_pulls/       # Processed outputs from 00_pull.ipynb — committed to GitHub
│   └── cleaned_data/   # Analysis-ready outputs from 01_clean.ipynb & 03_clean_proximity.ipynb
└── output/             # Output figures (PNG) — committed to GitHub
```

---

## Notebooks

Run notebooks in order. Each notebook lists its inputs and outputs below.

| Notebook | Description | Inputs | Outputs |
|----------|-------------|--------|---------|
| `code/00_pull.ipynb` | Loads all raw source files, filters to NJ, saves slim versions | `data/raw/` (large files — see below) | `data/01_pulls/*.csv`, `data/01_pulls/*.geojson` |
| `code/01_clean.ipynb` | Merges PFAS, census, and Zillow data by ZIP code; flags MCL exceedances | `data/01_pulls/` | `data/cleaned_data/final_map.csv`, `data/cleaned_data/final_clean_census.csv` |
| `code/02_visualize.ipynb` | ZIP-level maps, scatter plots, Pearson correlations, regression, box plots | `data/cleaned_data/final_map.csv` | `output/*.png` |
| `code/03_clean_proximity.ipynb` | Spatially joins ECHO facilities to PWS service areas; merges PFAS + demographics at water system level | `data/01_pulls/`, `data/cleaned_data/final_clean_census.csv` | `data/cleaned_data/proximity_final.geojson`, `data/cleaned_data/proximity_final.csv`, `data/cleaned_data/echo_facilities_with_pws.csv` |
| `code/04_visualize_proximity.ipynb` | Water system-level maps, t-tests, bar charts, scatter plots for proximity analysis | `data/cleaned_data/proximity_final.*`, `data/cleaned_data/echo_facilities_with_pws.csv` | `output/*.png` |

---

## Pre-Processed Files (committed to GitHub — ready to use)

If you only want to run notebooks `01_clean.ipynb` through `04_visualize_proximity.ipynb`, all required inputs are already in `data/01_pulls/`:

| File | Description |
|------|-------------|
| `data/01_pulls/ucmr5_nj_slim.csv` | NJ-filtered PFAS occurrence data (UCMR5) |
| `data/01_pulls/zipcodes_raw.csv` | PWSID to ZIP code crosswalk |
| `data/01_pulls/census_race_raw.csv` | Census ACS DP05 race data for NJ ZCTAs |
| `data/01_pulls/census_income_raw.csv` | Census ACS S1901 income data for NJ ZCTAs |
| `data/01_pulls/nj_zcta_2024.geojson` | NJ ZIP code boundary shapes |
| `data/01_pulls/pws_boundaries_nj.geojson` | NJ public water system service area polygons |
| `data/01_pulls/pws_tract_crosswalk_nj.csv` | PWSID to Census tract crosswalk (with population weights) |
| `data/01_pulls/echo_pfas_facilities_nj.csv` | EPA ECHO PFAS-handling facility locations in NJ |
| `data/01_pulls/zhvi_nj.csv` | Zillow Home Value Index for NJ ZIP codes (December 2024) |

---

## Raw Source Files (too large for GitHub — download separately)

These files are too large and must be downloaded and manually hardcoded from a local computer before running `00_pull.ipynb`.
A link to access all of these files directly is here:
https://drive.google.com/drive/folders/16chMCsDAEOjsihWfeYvnC3JGhDkNuXH9?usp=drive_link

| File | Source | Size |
|------|--------|------|
| `data/raw/UCMR5_All_MA_WY.txt` | [EPA UCMR5](https://www.epa.gov/dwucmr/occurrence-data-unregulated-contaminant-monitoring-rule) | ~175 MB |
| `data/raw/tl_2024_us_zcta520/` | [Census TIGER](https://www.census.gov/cgi-bin/geo/shapefiles/index.php) | ~500 MB |
| `data/raw/PWS_Boundaries/Service_Areas_V_3_0.gpkg` | [EPA PWS Service Areas](https://www.epa.gov/waterdata/pws-service-area-boundaries) | ~650 MB |
| `data/raw/Zip_zhvi_uc_sfrcondo_tier_0.33_0.67_sm_sa_month.csv` | [Zillow Research](https://www.zillow.com/research/data/) | ~15 MB |

The Zillow file uses December 2024 values (`ZHVI_DATE = '2024-12-31'` in `00_pull.ipynb`) to align with the UCMR5 collection period (Jan 2023 to Dec 2025) and Census ACS 5-Year 2024 (covers 2020 to 2024).

---

## Data Sources

| Dataset | Description | Link |
|---------|-------------|------|
| EPA UCMR5 | PFAS measurements in public water systems | [epa.gov/dwucmr](https://www.epa.gov/dwucmr/occurrence-data-unregulated-contaminant-monitoring-rule) |
| Census ACS DP05 | Race and ethnicity by ZIP code (ZCTA) | [data.census.gov](https://data.census.gov) |
| Census ACS S1901 | Household income by ZIP code (ZCTA) | [data.census.gov](https://data.census.gov) |
| Census TIGER ZCTAs | ZIP code boundary shapefiles | [census.gov/geo/shapefiles](https://www.census.gov/cgi-bin/geo/shapefiles/index.php) |
| EPA PWS Service Areas | Public water system service area polygons + census tract crosswalk | [epa.gov/waterdata](https://www.epa.gov/waterdata/pws-service-area-boundaries) |
| EPA ECHO | PFAS-handling industrial facility locations and compliance data | [echo.epa.gov](https://echo.epa.gov) |
| Zillow ZHVI | Home value index by ZIP code (December 2024) | [zillow.com/research/data](https://www.zillow.com/research/data/) |

---

## Key Variables

| Variable | Description | Units |
|----------|-------------|-------|
| `mean_pfas` | Mean PFAS concentration per ZIP or water system | ug/L (ppb) |
| `max_pfas` | Maximum PFAS concentration per ZIP or water system | ug/L (ppb) |
| `exceeds_mcl_mean` / `exceeds_mcl_max` | Whether mean/max PFAS exceeds EPA MCL of 0.004 ug/L | Boolean |
| `pct_poc` | % people of color (100 minus % white alone) | % |
| `pct_black` / `pct_hispanic` | % Black / % Hispanic population | % |
| `hh_median_income` | Median household income | USD |
| `zhvi` | Zillow Home Value Index (Dec 2024) | USD |
| `has_facility` | Whether a PFAS-handling facility is located inside the water system service area | Boolean |

All PFAS values are in ug/L (parts per billion). The EPA MCL for PFAS is 0.004 ug/L.
