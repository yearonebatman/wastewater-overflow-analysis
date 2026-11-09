Markdown

# Wastewater Overflow & Hydrologic Analysis (East Tennessee)

An exploratory data science project investigating the empirical relationships between reported municipal wastewater overflows, antecedent precipitation, and localized streamflow dynamics across East Tennessee.

---

## 1. Project Overview

### Objective
This project examines whether measurable thresholds of rainfall accumulation and localized stream response predict reported sanitary sewer overflows (SSOs). By standardizing and merging environmental observations across agencies, we address:
- How much antecedent precipitation (1-, 3-, and 7-day cumulative) typically precedes a reported overflow.
- The lag time between peak precipitation/stream crests and documented overflow occurrences.
- Spatial recurrence patterns across municipal sewer basins.

### Motivation
Wastewater overflows discharge untreated or partially treated sewage into regional creeks and river networks, posing direct risks to recreation and drinking water downstream. While wet-weather infiltration and inflow (I&I) are recognized causes, the underlying data remains fragmented across regulatory, hydrologic, and meteorological agencies. This project aggregates those disparate records into a unified, reproducible dataset to model antecedent conditions.

---

## 2. Data Sources & Specifications

| Domain | Agency / Source | Access Method | Expected Volume | Key Challenges |
| :--- | :--- | :--- | :--- | :--- |
| **Overflow Reports** | Tennessee Dept. of Environment and Conservation (TDEC) | Web exports / CSV batch queries | ~3,000 incident records (5–10 yr window) | Inconsistent timestamp precision (date-only vs. hour), missing volume estimates, duplicate entries. |
| **Stream Hydrology** | USGS National Water Information System (NWIS) | REST API (`dataretrieval` library) | ~2,000,000 rows (15-min gauge height & discharge) | Gauge telemetry outages during flood stages; spatial misalignment with outfalls. |
| **Meteorology** | NOAA NCEI / Local Climatological Data (LCD) | NOAA CDO REST API & bulk archives | ~300,000 hourly/daily observations | Localized convective rainstorms missing regional gauges; differentiating true zero rain from missing sensor logs. |

---

## 3. Project Structure

```text
wastewater-overflow-analysis/
├── data/
│   ├── raw/             # Read-only original source downloads (excluded from Git)
│   ├── interim/         # Cleaned subsets, timezone-aligned records (Parquet)
│   └── processed/       # Merged analysis-ready tables
├── figures/             # Output plots, maps, and reporting figures
├── notebooks/
│   ├── exploratory/     # Team sandbox and EDA notebooks
│   └── reports/         # Reproducible notebooks generating final deliverables
├── src/
│   ├── acquisition/     # API retrieval and data download scripts
│   ├── processing/      # Cleaning, deduplication, and geospatial matching
│   └── analysis/        # Feature engineering and classification modeling
├── .gitignore
├── README.md
└── requirements.txt
