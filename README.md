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
