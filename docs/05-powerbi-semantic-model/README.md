# 05 — Power BI Semantic Model

## Goal
Create a high-performance semantic model
that supports analytical and operational use cases.

The focus is on **model correctness first**, not DAX tricks.

---

## Modeling strategy
- Star schema
- Single-direction relationships
- Dedicated Date and Hour dimensions
- Measures over calculated columns

---

## Fact table
- gold_fact_energy_hourly

Grain:
- One row per hour per building

Contains:
- Energy (kWh, kW)
- PV generation
- Grid import/export
- HVAC metrics
- Occupancy
- Weather
- Tariff
- CO₂ emissions
- Cost (€)

---

## Dimensions
- gold_dim_date  
  (calendar logic, time intelligence)
- gold_dim_hour  
  (hour, daypart, business hours)
- gold_dim_building  
  (metadata: area, HVAC type, location)

---

## Star schema — model view
![Power BI model](../../assets/screenshots/powerbi/powerbi_model_star_schema.png)

---

## Measure-first approach
Core KPIs are implemented as measures:

- Total Energy (kWh)
- Total Cost (€)
- Total CO₂ (kg)
- Peak Demand (kW)
- Load Factor

![Measures overview](../../assets/screenshots/powerbi/powerbi_measures_overview.png)

---

## Why this matters
- Predictable filter behavior
- Clean time intelligence
- High performance on large datasets
- Easy extensibility for new KPIs
