# 04 — Fabric Bronze/Silver/Gold
# 04 — Fabric Medallion Architecture (Bronze / Silver / Gold)

## Goal
Transform raw landing data into a clean, analytics-ready
model optimized for Power BI and operational analytics.

The design follows a classic **Medallion Architecture**.

---

## Bronze — Raw ingestion
Bronze tables represent the landing data
with minimal transformation.

Characteristics:
- Schema alignment
- Timestamp normalization
- No joins
- Full traceability to source files

Examples:
- bronze_energy
- bronze_pv
- bronze_grid
- bronze_occupancy
- bronze_hvac
- bronze_tariff
- bronze_co2

---

## Silver — Conformed hourly fact
Silver is the **single source of truth**.

Key principles:
- One row = one hour
- Energy timeline as the primary axis
- All domains aligned to hourly grain

Main table:
- silver_fact_energy_hourly

Includes:
- Energy (kWh, kW)
- PV generation
- Grid import/export
- Occupancy
- Weather
- Tariff
- CO₂ intensity

---

## Gold — BI-ready star schema
Gold tables are optimized for Power BI.

Fact:
- gold_fact_energy_hourly

Dimensions:
- gold_dim_date
- gold_dim_hour
- gold_dim_building

Design choices:
- Star schema (no snowflake)
- Single-direction relationships
- Measures over calculated columns

---

## Fabric Lakehouse — table overview
![Fabric tables](../../assets/screenshots/fabric/fabric_lakehouse_tables_medallion.png)

---

## Gold fact & dimensions
![Gold model](../../assets/screenshots/fabric/gold_fact_and_dimensions_overview.png)

---

## Why this matters
- Clear separation of concerns
- Reusable analytics layer
- High Power BI performance
- Production-grade data modeling
