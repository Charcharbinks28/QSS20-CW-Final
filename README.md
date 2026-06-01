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

> ⚠️ **The raw source files are too large for GitHub and are NOT included in this repo.**
> The full UCMR5 dataset is ~175MB. Only the pre-processed, NJ-filtered outputs are committed.
> See instructions below to download the raw files if you want to re-run notebook 01 from scratch.

---

## Data

### Pre-processed files (committed to repo — ready to use)
These are already in `data/` and are all you need to run notebooks 02 and 03:

| File | Description |
|------|-------------|
| `data/ucmr5_nj_slim.csv` | NJ-filtered PFAS occurrence data (56,542 rows) |
| `data/zipcodes_raw.csv` | ZIP code to water system mapping |
| `data/census_raw.csv` | Census ACS DP05 demographics for NJ ZCTAs |
| `data/nj_zcta_2024.geojson` | NJ ZIP code boundary shapes |

### Raw source files (too large for GitHub — download separately)
Only needed to re-run `01_data_pull_me_search.ipynb`. Download and place in `data/raw/`:

| File | Source | Size |
|------|--------|------|
| `UCMR5_All_MA_WY.txt` | [EPA UCMR5](https://www.epa.gov/dwucmr/occurrence-data-unregulated-contaminant-monitoring-rule) | ~175MB |
| `UCMR5_ZIPCodes.txt` | [EPA UCMR5](https://www.epa.gov/dwucmr/occurrence-data-unregulated-contaminant-monitoring-rule) | ~0.5MB |
| `ACSDP5Y2024.DP05-Data.csv` | [Census Bureau](https://data.census.gov) | ~1MB |
| `tl_2024_us_zcta520/` (folder) | [Census TIGER](https://www.census.gov/cgi-bin/geo/shapefiles/index.php) | ~500MB |

---

## Outputs

- `output/nj_pfas_map.png` – Choropleth map of mean PFAS concentration by ZIP code in New Jersey.
- `output/nj_pfas_vs_race_map.png` – Map comparing PFAS levels against racial composition by ZIP code.
