
# Exploring Car Accidents in Chicago

A comprehensive exploratory data analysis (EDA) of Chicago traffic crash data, combining temporal, spatial, and demographic analysis to uncover patterns behind traffic accidents across the city.

---

## Overview

Using the City of Chicago's public Traffic Crashes datasets (crashes, vehicles, and people records), this project investigates *when*, *where*, and *under what conditions* traffic accidents are most likely to occur — combining statistical testing with geospatial analysis to support data-driven road safety insights.

---

## Data

Three linked datasets from the [Chicago Data Portal](https://data.cityofchicago.org):
- **Traffic Crashes** — crash-level details (date, time, weather, lighting, road conditions, contributory cause, damage)
- **Traffic Crashes – Vehicles** — vehicle-level details (make, model, year, defects)
- **Traffic Crashes – People** — person-level details (age, sex, injury classification, role)

Supplemented with geospatial reference layers: Chicago street center lines, police beat boundaries, and the Central Business District (CBD) boundary.

---

## Key Features

### Data Cleaning & Preparation
- Missing value imputation (mean for numeric, mode for categorical)
- Outlier handling via IQR-based clipping
- Column standardization and multi-table merging on crash/vehicle/person IDs

### Feature Engineering
- Vehicle age categorization (new / old / mixed) derived from crash date vs. manufacture year
- Passenger count and average passenger age per crash
- Street length categorization (short / medium / long) from geometric line length

### Geospatial Analysis
- **Geohashing** of crash coordinates to identify high-density crash zones
- **Distance-to-CBD calculation** using GeoPandas with CRS reprojection (EPSG:4326 → EPSG:6933) for accurate metric distance measurement
- Choropleth-style crash density visualization by geographic sector

### Temporal Analysis
- Crash frequency by hour, day of week, month, and year (trend analysis, including a visible COVID-19-related dip in 2020)
- Distribution analysis of monthly crash counts across years

### Statistical Testing
- Chi-square tests of independence to examine associations between:
  - Street length category and distance from CBD
  - Driver age category and vehicle age category

### Arabic-Language Visualization Support
- Full RTL Arabic label rendering in all charts using `arabic_reshaper` and `python-bidi`

---

## Key Findings

- Crash frequency is strongly associated with proximity to the Central Business District — crash counts decline as distance from the CBD increases.
- The most common contributory causes were impaired driving, reckless/aggressive driving, and failure to comply with traffic signals.
- Crashes are more frequent in low-light conditions, particularly on highways and major roads.
- Statistically significant associations were found between vehicle age and driver age categories.

---

## Tech Stack

**Data Processing:** Pandas, NumPy

**Geospatial Analysis:** GeoPandas, Shapely, geohash2

**Statistical Testing:** SciPy (Chi-square tests)

**Visualization:** Matplotlib, Seaborn, Plotly Express

**Arabic Text Support:** arabic_reshaper, python-bidi

---

## Project Structure

```
Chicago.ipynb           # Full analysis pipeline: cleaning → feature engineering → spatial/temporal analysis
Dataset_README.md       # Column-level documentation for all three datasets
```


**ملاحظة:** هالمشروع فعلياً بيستاهل يترفّع بالترتيب اللي حددناه سابقاً — بسبب المكون الجيومكاني القوي (geohashing، إسقاطات جغرافية، تحليل مكاني) اللي بيدعم مباشرة خلفيتك بـQGIS المذكورة بالـProfile. ممكن نفكر نحطه **رابع** (بعد Network Traffic وFinancial Assistant وMedical Texts)، قبل Traffic Signs وDiamond Price.

جاهز نثبت هيك، أو تعدل عليها؟
