# Smart Building EnergyOps — End-to-End Scenario

## Project overview
This project demonstrates an **end-to-end EnergyOps analytics platform**
for a smart building / campus environment.

The focus is not only on dashboards,
but on the **entire data lifecycle**:
from ingestion to analytics to automated operational actions.

---

## Scenario
A medium-sized educational campus is monitored to understand,
optimize, and operate its energy systems.

### Building profile
- Location: Berlin, Germany
- Building type: Educational campus
- Floor area: ~18,000 m²
- Peak occupancy: ~1,700 people
- HVAC system: Air-source heat pumps
- PV capacity: ~600 kWp
- Time resolution: Hourly

---

## Key questions addressed
- How does energy demand behave over time?
- When and why do peaks occur?
- How effectively is on-site PV utilized?
- What are the cost and carbon implications?
- Where are operational inefficiencies?
- What concrete actions can reduce energy and emissions?

---

## Architecture overview
The solution follows a production-grade analytics architecture:

**n8n → Azure / OneLake → Microsoft Fabric (Bronze/Silver/Gold)
→ Power BI (Semantic Model + Dashboards)
→ Automation & Alerts (Telegram)**

Each layer is documented step-by-step in this repository.

---

## Outcomes
- Unified hourly energy fact table
- BI-ready star schema
- Action-oriented dashboards
- Automated monitoring and alerts
- Clear path from data to decisions

---

## Why this project matters
This case study reflects how modern energy analytics
can move beyond reporting
towards **operational intelligence and automation**.

It is designed to resemble
real-world EnergyOps and smart building platforms.
