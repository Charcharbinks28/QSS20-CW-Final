# Data

Raw data files are too large for GitHub and are stored in Google Drive.

## Access Data Here
https://drive.google.com/drive/folders/1M2uRL4k4hyKPTdS0n9l7diCPBdZRrPjg?usp=sharing

## Files Needed
| `UCMR5_All_MA_WY.txt` | EPA UCMR5 PFAS occurrence data | [EPA UCMR](https://www.epa.gov/dwucmr) |
| `UCMR5_ZIPCodes.txt` | ZIP code to water system mapping | [EPA UCMR](https://www.epa.gov/dwucmr) |
| `ACSDP5Y2024.DP05-Data.csv` | Census ACS DP05 NJ demographics | [Census Bureau](https://data.census.gov) |

## To set up data, follow this:
1. Click the Google Drive link above
2. Download all files
3. Create a `data/raw/` folder at the root of this repo
4. Place `UCMR5_All_MA_WY.txt`, `UCMR5_ZIPCodes.txt`, and `ACSDP5Y2024.DP05-Data.csv` inside `data/raw/`
5. For the shapefile, extract the `tl_2024_us_zcta520` folder into `data/raw/tl_2024_us_zcta520/`

The processed outputs (`ucmr5_nj_slim.csv`, `zipcodes_raw.csv`, `census_raw.csv`, `nj_zcta_2024.geojson`) are already committed to the repo — you only need the raw files if you want to re-run notebook 01 from scratch.
