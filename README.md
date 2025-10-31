# DSA 210 Term Project: Crime Rate Prediction

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

---

## Where the Data Comes From & How I’ll Collect It

I start with U.S. cities because open data is easy to access. (I can later repeat the idea at the **country** level.)

### A) Crime Data (City Portals)

Here below there are some example ways and cities that I will be incorporating in my project:

* **Chicago** — https://catalog.data.gov/dataset/crimes-2001-to-present?utm_source=
* **New York City** — https://www.nyc.gov/site/nypd/stats/crime-statistics/historical.page
* **Los Angeles** — *Crime Data from 2020 to Present* (LA Open Data). I export CSV; columns include crime code, area, date.

**Target I create**: `crime_rate_per_100k = (crime_count / population) * 100000` for the same city & year.

### B) Socio‑economic & Demographic Features 

All from **U.S. Census – American Community Survey (ACS, 5‑year)** at **place** level (city/town). I’ll download CSVs and use the **Census API** with these tables:

Links below are one example from a city in United States, because I'll be manipulating for each state therefore it would be inconvenient to list over 20 states' api below.

1. **Poverty rate (%)** — [https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S1701_C03_001E&for=place:*&in=state:06](https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S1701_C03_001E&for=place:*&in=state:06)
2. **Unemployment rate (%)** — [https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S2301_C04_001E&for=place:*&in=state:06](https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S2301_C04_001E&for=place:*&in=state:06)
3. **Educational attainment (% BA+)** — [https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S1501_C02_015E&for=place:*&in=state:06](https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S1501_C02_015E&for=place:*&in=state:06)
4. **Median household income (USD)** — [https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S1901_C01_012E&for=place:*&in=state:06](https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S1901_C01_012E&for=place:*&in=state:06)
5. **Population density (people/km²)** — [https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S0101_C01_001E&for=place:*&in=state:06](https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S0101_C01_001E&for=place:*&in=state:06)
6. **Public transit commute share (%)** — [https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S0801_C01_086E&for=place:*&in=state:06](https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S0801_C01_086E&for=place:*&in=state:06)
7. **Residential mobility (% different house 1 year ago)** — [https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S0701_C04_001E&for=place:*&in=state:06](https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S0701_C04_001E&for=place:*&in=state:06)
