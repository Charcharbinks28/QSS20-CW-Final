# QSS20-CW-Final
# PFAS Contamination and Racial Disparities in New Jersey

## Project Overview

This project investigates whether PFAS (per- and polyfluoroalkyl substances) contamination in New Jersey drinking water is disproportionately concentrated in communities of color. Using data from the EPA's Unregulated Contaminant Monitoring Rule (UCMR 5), ZIP code-level demographic data from the U.S. Census, and New Jersey geographic shapefiles, this analysis examines the relationship between PFAS exposure levels and racial composition across NJ ZIP codes.


## Scripts

| Notebook | Description |
|----------|-------------|
| `code/01_data_pull.ipynb` | Pulls raw data from EPA UCMR 5, NJ ZIP code shapefile, and Census API. Saves raw CSVs to `data/`. |
| `code/02_visualize.ipynb` | Merges PFAS and demographic data, generates maps and figures saved to `output/`. |

---

## Data Sources

- **EPA UCMR 5** – Unregulated Contaminant Monitoring Rule data on PFAS levels in public water systems. [EPA UCMR 5 Data](https://www.epa.gov/dwucmr/occurrence-data-unregulated-contaminant-monitoring-rule)
- **U.S. Census Bureau** – ZIP code-level demographic data (race, population) via the Census API.
- **NJ ZCTA Shapefile** – New Jersey ZIP Code Tabulation Areas (2024) for geographic mapping.

> Raw data files are stored in the `data/` folder of this repository.

---

## Outputs

- `output/nj_pfas_map.png` – Choropleth map of mean PFAS concentration by ZIP code in New Jersey.
- `output/nj_pfas_vs_race_map.png` – Map comparing PFAS levels against racial composition by ZIP code.
