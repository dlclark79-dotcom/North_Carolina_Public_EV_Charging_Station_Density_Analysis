# North Carolina Public EV Charging Station Density Analysis

## Project Overview
As part of my data analytics learning journey, I built this project to practice data cleaning in R, data normalization, and spatial mapping in Tableau. 

The goal of this study is to compare public EV charging station density across North Carolina relative to population size, helping identify which ZIP codes currently have high or low charging infrastructure per capita.

---

## Data Sources & Tools

### Data Sources
* **US Department of Energy (AFDC):** EV charging station locations and operational data ([Link](https://driveelectric.gov/stations)).
* **US Census Bureau:** 2020 Decennial Census county and ZIP code population totals ([Link](https://www.census.gov/)).

### Tech Stack Used
* **RStudio (R):** Used for standardizing column names (`snake_case`) and checking for missing/null values. 
* **MySQL Workbench:** Used for calculating population-weighted metrics and generating a summary table to be used in Tableau.
* **Tableau Public:** Used to generate a static spatial visualization map.

---

## Data Scoping & Cleaning Process

### 1. Scoping to North Carolina
To avoid manually downloading and combining individual files for all 50 states, I scoped this initial analysis specifically to the state of North Carolina.

### 2. Cleaning in R
Both datasets were imported into RStudio to inspect quality:
* Standardized all variable names to `snake_case` for consistency.
* Evaluated null values. While the charging station table contained missing entries in some fields, all critical fields needed for location and ID counts were 100% complete.

### 3. Metric Normalization (SQL)
Because raw station counts naturally favor densely populated areas, I normalized the data to evaluate **charging stations per 1,000 residents**:


$$\text{Stations per 1,000 Residents} = \left( \frac{\text{ZIP Code Station Count}}{\text{ZIP Code Population}} \right) \times 1,000$$

---

## Analysis & Findings

Looking at North Carolina overall (10,439,413 residents and 90 public stations in this dataset), the statewide average is very low on a per-capita basis. 

When comparing individual ZIP codes against the state average:
* **ZIP codes with higher relative density:** `27964`, `27601`, and `27959` showed higher proportions of stations relative to their population base.
* **ZIP codes with lower relative density:** Highlighted red on the map (Figure 1), `28078`, `27519`, and `28025` represent areas where station availability lags behind local population size.

*(Insert Figure 1 Image Here)*

---

## Key Limitations & What I Learned

This project was a great learning experience, and it highlighted several real-world data limitations I would address in future iterations:

1. **Census Data Age:** The 2020 Census data is a few years old and does not capture recent state population migration.
2. **Unserved ZIP Codes:** This current draft only evaluates ZIP codes that already have at least one charging station. It excludes ZIP codes with zero stations, which might actually be the highest-priority "charging deserts."
3. **Next Steps for Growth:** To expand this project, I would like to pull in state EV registration counts to see where EV owners actually live, rather than relying solely on general population size.
