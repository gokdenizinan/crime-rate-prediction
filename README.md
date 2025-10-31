# Crime Rate Prediction

I use **socio‑cultural and economic features** together with **crime data** to train a simple machine‑learning model. After training on some cities (or countries), I want to enter a **new place** and get a **predicted crime rate**.

---

## What this project does

* Brings crime data and city stats into one clean table (same year, same city IDs).
* Tests which features relate most to crime.
* Trains a small model (Linear Regression → Random Forest) and checks its accuracy.
* Lets me predict a crime rate for a city/country the model hasn’t seen.

---

## Data sources I plan to use

You can start with one city (Chicago is an easy example) and then add more.

### Crime data (city portals)

* **Chicago** — *Crimes – 2001 to Present* (Chicago Data Portal). Columns: date, primary_type, ward, community_area, etc.
* **New York City** — *NYPD Complaint Data (Historic / Current)* (NYC Open Data). Columns: offense, boro, precinct, latitude/longitude.
* **Los Angeles** — *Crime Data from 2020 to Present* (LA Open Data). Columns: crime code, area, date, lat/long.

> I convert raw counts to **crime_rate_per_100k** using city population.

### City indicators (U.S.)

All of these are available from **U.S. Census – American Community Survey (ACS, 5‑year)** at **place** level (city/town). I also added a quick pointer to an example “database/table” name you can look up.

1. **Poverty rate (%)**
   *Source:* ACS **S1701** (Poverty Status).
   *Example fields:* `S1701_C03_001E` (percent below poverty).

2. **Unemployment rate (%)**
   *Source:* ACS **S2301** (Employment Status).
   *Example fields:* `S2301_C04_001E` (unemployment %).

3. **Educational attainment (% BA or higher)**
   *Source:* ACS **S1501** (Education).
   *Example fields:* `S1501_C02_015E` (bachelor’s degree or higher, % of 25+).

4. **Median household income (USD)**
   *Source:* ACS **S1901** (Income).
   *Example fields:* `S1901_C01_012E` (median household income).

5. **Population density (people per km²)**
   *Source:* ACS **S0101** (total population) + **Census Gazetteer** (land area).
   *How I compute:* `population / land_area_km2` (often I log‑transform density).

6. **Public transit commute share (%)**
   *Source:* ACS **S0801** (Commuting).
   *Example fields:* `S0801_C01_086E` (public transportation to work, %).

7. **Residential mobility (% lived in a different house 1 year ago)**
   *Source:* ACS **S0701** (Geographic Mobility).
   *Example fields:* `S0701_C04_001E` (moved from a different house, %).

> I align all indicators to the **same reference year** as the crime data. If cities lack some fields, I keep the model simple and drop or impute carefully.

### Optional (country level)

If I test countries instead of cities:

* **Crime index by country** — datasets similar to Numbeo/Kaggle "World Crime Index".
* **World Bank indicators** — use the API with indicator codes like `NY.GDP.PCAP.CD` (GDP per capita), `SE.ADT.LITR.ZS` (literacy), `SP.URB.TOTL.IN.ZS` (urbanization), `SL.UEM.TOTL.ZS` (unemployment), `SP.POP.TOTL` (population).

---

## Method (short and simple)

1. **Collect & clean**: load CSVs, fix city names/IDs (GEOID if using ACS), keep one row per city per year.
2. **Explore**: quick charts and a basic correlation check.
3. **Features**: keep 5–7 useful fields; log density if it’s very skewed.
4. **Train**: start with Linear Regression, then try Random Forest.
5. **Evaluate**: train/test split; report **R²** and **RMSE/MAE**.
6. **Predict**: given a new city’s features, output a predicted `crime_rate_per_100k`.

---

## Project structure

```
.
├─ data/
│  ├─ raw/          # original files
│  └─ processed/    # clean/merged data
├─ notebooks/
│  ├─ 01_eda.ipynb
│  └─ 02_model.ipynb
├─ src/
│  ├─ load_and_clean.py
│  ├─ build_features.py
│  └─ train_model.py
├─ reports/
│  └─ figures/
├─ requirements.txt
└─ README.md
```

---

## How to run

1. Create the environment and install:

```bash
python -m venv .venv
# macOS/Linux
source .venv/bin/activate
# Windows
# .venv/Scripts/activate
pip install -r requirements.txt
```

2. Put source CSVs into `data/raw/`, then build and train:

```bash
python src/load_and_clean.py
python src/build_features.py
python src/train_model.py
```

3. Or open the notebooks and run step by step.

---

## Model I/O

**Inputs (example, city level)**

```
poverty_rate,unemployment_rate,ba_or_higher_share,median_household_income,population_density,transit_commute_share,mobility_rate_1yr
18.2,7.1,27.4,52000,4300,12.6,16.9
```

**Target**: `crime_rate_per_100k`

**Outputs**: test scores (R², RMSE/MAE), feature importance/weights, and a small function that predicts a new city’s crime rate.

---
