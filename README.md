# DSA 210 Term Project: Crime Rate Prediction

<h3 align="center">Do city stats explain crime, and can we predict a new city's rate?</h3>

This project uses simple **socio‑cultural and economic features** together with **crime data** to train a model. After learning from a set of cities, the goal is to enter a **new city (or country)** and get a **crime‑rate estimate**.

---

## Research Question

**Can a small set of city features (income, education, unemployment, density, transit use, etc.) explain and predict crime rates across cities?**

### Sub‑Questions

* Which features show the strongest relationship with crime rate?
* If I hold out entire cities, can the model still predict their crime rate reasonably well?
* Do results support ideas like “higher income → lower crime” or “higher density → higher crime”?

### Hypotheses

* **H1:** Cities with **higher education (BA+)** have **lower** crime rates.
* **H2:** **Higher poverty** and **higher unemployment** relate to **higher** crime rates.
* **H3:** **Population density** and **transit commute share** are **positively** related to crime rate, but the effect weakens after adding other features.

---

## How I Will Test

1. **Build one clean table**: one row per city per year with target `crime_rate_per_100k` and 5–7 features.
2. **Train/Test split by city**: hold out whole cities (not random rows) to see if the model generalizes.
3. **Models**: start with **Linear Regression**; compare with **Random Forest**.
4. **Metrics**: report **R²** and **MAE/RMSE** on the held‑out cities; compare models.
5. **Feature checks**: look at coefficients (linear) or feature importance (forest) to evaluate H1–H3.
6. **New‑city demo**: plug in features for a city not in training and output a predicted crime rate.

> Keep it simple: small feature set, same year for all fields, and basic plots to sanity‑check results.

---

## Where the Data Comes From & How I’ll Collect It

I start with U.S. cities because open data is easy to access. (I can later repeat the idea at the **country** level.)

### A) Crime Data (City Portals)

Pick one or more:

* **Chicago** — *Crimes – 2001 to Present* (Chicago Data Portal). I export CSV by year; columns include date, offense type, community area.
* **New York City** — *NYPD Complaint Data* (NYC Open Data). I export CSV; columns include offense, borough, precinct, lat/long.
* **Los Angeles** — *Crime Data from 2020 to Present* (LA Open Data). I export CSV; columns include crime code, area, date.

**Target I create**: `crime_rate_per_100k = (crime_count / population) * 100000` for the same city & year.

### B) Socio‑economic & Demographic Features (ACS, Place Level)

All from **U.S. Census – American Community Survey (ACS, 5‑year)** at **place** level (city/town). I’ll download CSVs or use the **Census API** with these tables:

1. **Poverty rate (%)** — ACS **S1701** (e.g., `S1701_C03_001E`)
2. **Unemployment rate (%)** — ACS **S2301** (e.g., `S2301_C04_001E`)
3. **Educational attainment (% BA+)** — ACS **S1501** (e.g., `S1501_C02_015E`)
4. **Median household income (USD)** — ACS **S1901** (e.g., `S1901_C01_012E`)
5. **Population density (people/km²)** — ACS **S0101** (population) + **Census Gazetteer** (land area) → `pop/land_area_km2`
6. **Public transit commute share (%)** — ACS **S0801** (e.g., `S0801_C01_086E`)
7. **Residential mobility (% different house 1 year ago)** — ACS **S0701** (e.g., `S0701_C04_001E`)

**Year alignment**: choose one reference year (e.g., 2022) and match all features and crime counts to that year. If a feature is missing for a city, I keep the model simple and drop that city/feature rather than guessing.

### Optional (Country Level)

* **Crime index by country** (Numbeo/Kaggle‑style datasets).
* **World Bank indicators (API)**: `NY.GDP.PCAP.CD` (GDP per capita), `SE.ADT.LITR.ZS` (literacy), `SP.URB.TOTL.IN.ZS` (urbanization), `SL.UEM.TOTL.ZS` (unemployment), `SP.POP.TOTL` (population). Merge by country and year.
