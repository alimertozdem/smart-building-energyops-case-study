# Data Model (v2)

This document describes the Gold-layer star schema used by Smart Building EnergyOps (v2),
centered around a canonical hourly fact table.

## 1) Grain & Keys (most important)

**Fact grain:** 1 row = **1 building × 1 hour**  
**Primary keys:** `building_id`, `dt_timestamp` (UTC)

> Industry phrasing: *“define the grain first”, “timestamp as the join key”, “UTC to avoid DST ambiguity”.*

---

## 2) Fact Table (Gold)

### Canonical fact
**Table:** `gold_fact_energy_hourly`  
(If a dispatch-specific variant exists, it must keep the same contract + keys.)

**Core columns (examples)**
- Identifiers: `building_id`, `dt_timestamp`
- Energy: `energy_kwh`, `energy_kw`
- Grid: `grid_import_kwh`, `grid_export_kwh`, `net_grid_kwh`
- PV: `pv_kwh`, `pv_kw`
- Battery (BESS): `bess_charge_kwh`, `bess_discharge_kwh`, `bess_soc_pct`
- HVAC: `hvac_kwh`, `hvac_kw`, `deltaT_c`, `cop`
- Comfort: `indoor_temp_c`, `setpoint_temp_c`, `comfort_in_band_flag`, `comfort_deviation_c`
- Weather: `outside_temp`, `humidity`, `weather_solar_irradiance`
- Economics: `price_eur_per_kwh`, `cost_eur`
- Carbon: `co2_g_per_kwh`, `co2_kg`
- Ops: `occupancy`

> Industry phrasing: *“canonical schema contract”, “nullable by capability”, “business-ready fact table”.*

---

## 3) Dimensions (Gold)

### `gold_dim_building`
**Key:** `building_id`  
Contains: building_name, type, location, floor_area_m2, pv/bess capacities, etc.

**Why it exists**
- enables multi-building comparisons
- avoids repeating attributes in the fact

> Industry phrasing: *“conformed dimension”, “attribute table”.*

### `gold_dim_date`
**Key:** `date`  
Contains: year, month, weekday, is_weekend, etc.

> Industry phrasing: *“calendar dimension”, “date intelligence”.*

### `gold_dim_hour`
**Key:** `hour`  
Contains: daypart, business_hours_flag, peak_hours_flag, etc.

> Industry phrasing: *“time-of-day segmentation”, “daypart dimension”.*

---

## 4) Relationships (Star Schema)

- Fact → Building: `gold_fact_energy_hourly[building_id]` → `gold_dim_building[building_id]`
- Fact → Date: `DATE(dt_timestamp)` (or an existing date column) → `gold_dim_date[date]`
- Fact → Hour: `HOUR(dt_timestamp)` (or an existing hour column) → `gold_dim_hour[hour]`

**Model hygiene**
- single-direction filters (dim → fact)
- avoid bi-directional relationships unless justified

> Industry phrasing: *“star schema”, “single-direction relationship”, “filter propagation”.*

---

## 5) Notes on Timezones & DST

- `dt_timestamp` is stored and joined in **UTC**
- local timezone is used only for reporting/UX (Berlin time)
- prevents duplicate/missing hours during DST transitions

> Industry phrasing: *“DST-safe timestamps”, “UTC as source of truth”.*

---

## 6) Measure Strategy (Power BI)

- Prefer **measures** over calculated columns for aggregations
- Create measures in a dedicated table (e.g., `Measures_V2`)
- Keep naming consistent: `V2 <Metric Name> (...)`

> Industry phrasing: *“semantic layer measures”, “measure table”, “naming conventions”.*
