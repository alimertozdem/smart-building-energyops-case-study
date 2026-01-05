
# System Architecture (v2)

This document describes the high-level architecture of the Smart Building EnergyOps project,
with a focus on the Fabric-first v2 design.

## 1) Architecture Summary

**Goal:** Build a production-minded, end-to-end energy analytics + optimization case study using Microsoft Fabric as the core platform.

**Key principles**
- **Fabric-first:** ingestion, transformation, and modeling happen inside Fabric
- **Canonical fact table:** one stable hourly fact schema across buildings
- **Star schema:** clean dimensions for Date / Hour / Building
- **Replaceable sources:** synthetic data can be swapped with authoritative APIs without breaking the model
- **Ops vs analytics separation:** n8n is used only for monitoring/alerts (not transformations)

> Industry phrasing: *“separation of concerns”, “single source of truth (SSOT)”, “canonical model”, “star schema”.*

---

## 2) High-Level Data Flow

APIs (Weather, ENTSO-E day-ahead prices)  
→ **Fabric Notebook (Python)**  
→ **Lakehouse** (Bronze → Silver → Gold)  
→ **Power BI Semantic Model**  
→ Dashboards (Energy Market, Economic Impact, Comfort & Ops)  
→ **n8n** (alerts & monitoring only)

### What each layer means (industry terms)

- **Bronze (Raw / Landing):** raw ingested API responses, minimal changes  
  *aka “landing zone”, “raw layer”*

- **Silver (Clean / Conformed):** cleaned data types, standardized timestamps, deduping, quality checks  
  *aka “conformed layer”, “validated layer”*

- **Gold (Business-ready):** analytics-ready tables (facts & dimensions), stable schema, KPI-ready  
  *aka “serving layer”, “semantic-ready layer”*

---

## 3) Ingestion & Orchestration

### Fabric Notebook (primary ingestion)
Used for:
- API calls (pagination, retry, rate limits)
- timestamp normalization (**UTC join key** to avoid DST ambiguity)
- synthetic-but-realistic energy generation (where needed)
- PV + Battery dispatch simulation logic

**Why notebooks (production-minded):**
- reproducible runs
- parameterized logic
- easier API handling than low-code tools

> Industry phrasing: *“idempotent loads”, “incremental ingestion”, “reproducible pipelines”.*

### n8n (operations only)
n8n is intentionally limited to:
- refresh failure alerts
- data freshness alerts
- KPI threshold alerts (peak demand, SOC thresholds)

> Industry phrasing: *“monitoring and alerting”, “ops automation”, “notification workflow”.*

---

## 4) Data Model (Gold)

### Canonical fact table (hourly grain)
**Table:** `gold_fact_energy_hourly` (or dispatch variant in later iterations)  
**Grain:** hourly  
**Keys:** `building_id`, `dt_timestamp` (UTC)

Contains measures for:
- energy & grid (import/export/net)
- PV generation
- battery (charge/discharge, SOC)
- HVAC & comfort metrics
- weather context
- cost (€/kWh, €) and carbon (kg CO₂)

### Dimensions (star schema)
- `gold_dim_building` (building attributes)
- `gold_dim_date` (calendar logic)
- `gold_dim_hour` (daypart, business hours, peak flag)

> Industry phrasing: *“star schema”, “fact grain”, “conformed dimensions”, “stable schema contract”.*

---

## 5) Serving: Power BI Semantic Model

Power BI sits on top of Gold tables:
- measures created in a dedicated measure table (e.g., `Measures_V2`)
- pages built to answer operational questions (not just charts)

**Typical model hygiene**
- single-direction relationships (dim → fact)
- measures over calculated columns when possible
- avoid reshaping fact tables in DirectQuery/Mixed scenarios unless necessary

> Industry phrasing: *“semantic layer”, “model hygiene”, “filter context”.*

---

## 6) Reliability & Validation

Minimum checks after each run:
- row counts by building & date range
- null-rate checks for critical columns (timestamp, building_id, energy_kwh)
- basic sanity rules (no negative energy_kwh, SOC between 0–100%)
- cost consistency (cost = kWh × price)

> Industry phrasing: *“data quality checks”, “sanity checks”, “validation pack”.*

---

## 7) What’s next (optional)

- replace synthetic prices with ENTSO-E once token is active
- add scenario comparisons (cost-optimized vs peak-optimized dispatch)
- annualized savings & payback
- CO₂ impact using market-based emission factors
