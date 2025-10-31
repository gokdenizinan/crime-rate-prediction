# DSA 210 Term Project: Crime Rate Prediction

This project uses simple **socio‑cultural and economic features** together with **crime data** to train a model. After learning from a set of cities, the goal is to enter a **new city (or country)** and get a **crime‑rate estimate**.

---

## Research Question

**Can a small set of city features (income, education, unemployment, density, transit use, etc.) explain and predict crime rates across cities?**

### Sub‑Questions

* Which features show the strongest relationship with crime rate?
* If I hold out entire cities, can the model still predict their crime rate reasonably well?
* Do results support ideas like “higher income → lower crime” or “higher density → higher crime”?

### Motivation
* As a person who fancies rading crime novels and like watching criminal tv series , as well as , films  I thought that trying to measure and predict crime rates in various cities would be a fun puzzle to solve. Therefore, I set various parameters which I think that are relevant for my project and in relation with crime records. As much as coding gives me joy while tackling some mysterious questions in life, I also wanted to incorporate criminal activities with some socio-cultural aspects in life and trying to see whether they have a relationship or not.

### Hypotheses

* **H1:** Cities with **higher education (BA+)** have **lower** crime rates.
* **H2:** **Higher poverty** and **higher unemployment** relate to **higher** crime rates.
* **H3:** **Population density** and **transit commute share** are **positively** related to crime rate, but the effect weakens after adding other features.

---
Mükemmel! 🎯
İşte son attığım **akademik ama sade** metnin GitHub reposunun `README.md` dosyasına uygun, Markdown formatında düzenlenmiş hali — başlık yapısı, okunabilirlik ve stil tamamen GitHub standartlarına uygun:

---

## 🧪 How I Will Test

1. **Build one dataset**
   I will combine all information into a single table.
   Each row will represent one city in one year, including its crime level and several social and economic features.

2. **Train and test the model**
   The model will be trained using data from some cities and tested on others.
   This will show whether it can predict crime levels for cities it has never seen before.

3. **Use two different models**
   I will start with a simple linear model and then test a more advanced one to compare their performance.

4. **Evaluate performance**
   I will measure how close the model’s predictions are to the actual crime levels and how well it explains the differences between cities.

5. **Identify key factors**
   I will examine which city features are most strongly related to crime rates.

6. **Apply to a new city**
   Finally, I will use the trained model to estimate the crime level for a new city that was not included in the training data.
   
---

## Where the Data Comes From & How I’ll Collect It


### A) Crime Data (City Portals)

Here below there are some example ways and cities that I will be incorporating in my project:

Links below are one example from a city in United States, because I'll be manipulating for each state therefore it would be inconvenient to list over 20 states' api below.

* **Chicago** — https://catalog.data.gov/dataset/crimes-2001-to-present?utm_source=
* **New York City** — https://www.nyc.gov/site/nypd/stats/crime-statistics/historical.page
* **Los Angeles** — *Crime Data from 2020 to Present* (LA Open Data). I export CSV; columns include crime code, area, date.


### B) Socio‑economic & Demographic Features 

All from **U.S. Census – American Community Survey (ACS, 5‑year)** at **place** level (city/town). I’ll download CSVs and use the **Census API** with these tables:


1. **Poverty rate (%)** — [https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S1701_C03_001E&for=place:*&in=state:06](https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S1701_C03_001E&for=place:*&in=state:06)
2. **Unemployment rate (%)** — [https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S2301_C04_001E&for=place:*&in=state:06](https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S2301_C04_001E&for=place:*&in=state:06)
3. **Educational attainment (% BA+)** — [https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S1501_C02_015E&for=place:*&in=state:06](https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S1501_C02_015E&for=place:*&in=state:06)
4. **Median household income (USD)** — [https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S1901_C01_012E&for=place:*&in=state:06](https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S1901_C01_012E&for=place:*&in=state:06)
5. **Population density (people/km²)** — [https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S0101_C01_001E&for=place:*&in=state:06](https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S0101_C01_001E&for=place:*&in=state:06)
6. **Public transit commute share (%)** — [https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S0801_C01_086E&for=place:*&in=state:06](https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S0801_C01_086E&for=place:*&in=state:06)
7. **Residential mobility (% different house 1 year ago)** — [https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S0701_C04_001E&for=place:*&in=state:06](https://api.census.gov/data/2023/acs/acs5/subject?get=NAME,S0701_C04_001E&for=place:*&in=state:06)
