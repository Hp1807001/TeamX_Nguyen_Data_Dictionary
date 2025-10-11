# ASIAS Preliminary Accident/Incident Data — Documentation (Redesigned)

**Primary source:** FAA Aviation Safety Information Analysis & Sharing (ASIAS) — Preliminary Accident and Incident Reports (CSV available): https://www.asias.faa.gov/apex/f?p=100:93:::NO

## Data Model (Proposed)
- **Fact:** `asias_preliminary_fact` (one row per notice)
- **Dimensions:** `lkp_manufacturer`, `lkp_model`, `lkp_phase_of_flight`, `lkp_weather`, `lkp_injury_severity`

## Keys
- `Notice_ID` is the primary key for the fact table.
- Foreign keys: `Make`, `Model`, `Phase_of_Flight`, `Weather_Condition`, `Injury_Severity` join to their respective lookup tables.

## Wrangling Plan
- Parse dates to ISO 8601; normalize text (trim, title/upper as needed).
- Normalize manufacturer/model values (case/spacing).
- Optional: geocode `Location` into `Latitude/Longitude` if not present.
- Validate PK uniqueness; enforce referential integrity to lookups.

## Storage & Serving
- Stage in SQLite (`asias_prelim` schema).
- Curated outputs as partitioned Parquet for analytics.
- Dashboards: Power BI (daily/weekly trends, manufacturer counts, event types).

> Replace the *template* columns in `ASIAS_Data_Dictionary.xlsx` with the exact columns from your downloaded CSV to finalize.
