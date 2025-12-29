# 06 — Dashboards & Analytics Story

This section presents the analytical layer built on top of the
semantic model.

Each dashboard page answers a **specific business question**.

---

## Executive Overview

### Business question
“How is the campus performing at a high level?”

### What this page shows
- Total Energy Consumption
- Total Cost (€)
- Total CO₂ Emissions
- Peak Demand
- Renewable Energy Contribution

The goal is to provide **one-glance visibility**
for decision makers.

---

### Executive Overview — Screenshot
![Executive Overview](../../assets/screenshots/powerbi/dashboard_executive_overview.png)




---

## PV & Grid Interaction

### Business question
“How effectively is on-site PV generation utilized,
and when does the building rely on the grid?”

### What this page shows
- PV generation over time
- Grid import vs export
- Interaction between load and on-site generation
- Daytime vs nighttime behavior

This page helps identify:
- PV self-consumption opportunities
- Grid dependency periods
- Potential storage or load-shifting use cases

---

### PV & Grid Interaction — Screenshot
![PV & Grid Interaction](../../assets/screenshots/powerbi/dashboard_pv_grid_interaction.png)

---

### Key insights enabled
- Alignment (or misalignment) between PV production and demand
- Periods of excess generation
- Opportunities to increase on-site utilization




---

## Load & Operations

### Business question
“When does energy demand peak and how consistent is the load profile?”

### What this page shows
- Hourly load profile (kW)
- Daily and weekly patterns
- Peak demand identification
- Base load behavior

This page helps identify:
- Operational inefficiencies
- Unexpected peaks
- Off-hours energy waste

---

### Load & Operations — Screenshot
![Load & Operations](../../assets/screenshots/powerbi/dashboard_load_operations.png)

---

### Key insights enabled
- Peak-hour risk detection
- Load smoothing opportunities
- Demand-side optimization potential


---

### Key design principles
- Minimal visual noise
- KPI-first layout
- Trends before breakdowns
- Business language, not technical metrics
