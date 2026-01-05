
This repository documents the evolution of the Smart Building EnergyOps project,
with a primary focus on the v2 Fabric-first architecture.

## Project Evolution: v1 → v2

| Area | v1 | v2 |
|-----|----|----|
| Platform | n8n + Azure | **Microsoft Fabric (end-to-end)** |
| Ingestion | n8n workflows | **Fabric Notebooks (Python)** |
| Modeling | Multiple fact tables | **Single canonical fact table** |
| Scope | Single building | **Multi-building** |
| Focus | Reporting | **Energy optimization & operations** |

In v2, n8n is intentionally limited to operational alerting only.
All core data engineering and transformations are handled natively in Microsoft Fabric.
## High-Level Architecture

APIs (Weather, Market Prices)
        ↓
Microsoft Fabric Notebooks
        ↓
Lakehouse (Bronze → Silver → Gold)
        ↓
Power BI Semantic Model
        ↓
Dashboards & Operational Insights


## What This Repository Includes

- Fabric notebooks for API ingestion and energy modeling
- Bronze / Silver / Gold lakehouse tables
- Canonical hourly energy fact table
- Power BI semantic model and dashboards
- Operational KPIs for energy, cost, and comfort

## What This Repository Is Not

- A real-time Energy Management System (EMS)
- A production controller for batteries or HVAC
- A generic Power BI demo dashboard

This project is a **decision-support simulation** designed to demonstrate
energy analytics and optimization logic.

## Why This Project Matters

This project demonstrates how modern data platforms like Microsoft Fabric
can be used not only to report energy data, but to **operate and optimize
energy systems** using market signals and operational constraints.



# Smart Building EnergyOps — End-to-End Case Study

End-to-end smart campus energy analytics platform:
**n8n → Azure/OneLake → Microsoft Fabric (Bronze/Silver/Gold) → Power BI (Star Schema) → Automations (Telegram)**

## What this repo includes
- Production-minded ingestion pipelines (hourly → monthly partitioned CSV exports)
- Lakehouse modeling (Bronze/Silver/Gold)
- Power BI semantic model (star schema + KPI measures)
- Executive & Ops dashboards (Energy, Cost, Carbon, PV, HVAC)
- Automation layer (refresh monitoring + Telegram alerts)

## Walkthrough (step-by-step)
1. [01 — Scenario](docs/01-scenario/README.md)
2. [02 — Ingestion (n8n)](docs/02-ingestion-n8n/README.md)
3. [03 — Landing (Azure/OneLake)](docs/03-landing-azure-onelake/README.md)
4. [04 — Fabric Bronze/Silver/Gold](docs/04-fabric-medallion/README.md)
5. [05 — Power BI Semantic Model](docs/05-powerbi-semantic-model/README.md)
6. [06 — Dashboards](docs/06-dashboards/README.md)
7. [07 — Automation & Alerts](docs/07-automation-alerts/README.md)
8. [08 — Lessons Learned](docs/08-lessons-learned/README.md)

## Status
- Pipeline: monthly exports for major domains (Energy, PV, Grid, Occupancy, HVAC, Tariff; CO₂ optional single file)
- Fabric: Bronze/Silver/Gold model in place
- Power BI: core pages implemented
- Automation: refresh monitoring + Telegram ops messaging
