# 07 — Automation & Alerts (EnergyOps)

## Goal
Move from passive analytics to **operational energy management**.

Dashboards are monitored automatically, and issues trigger alerts without manual checks.

---

## What was automated
- Daily EnergyOps summary (scheduled)
- Dataset refresh monitoring (silent on success, alert on failure)
- Data freshness checks
- Operational messaging via Telegram

---

## n8n automation workflow
This workflow orchestrates the decision-support logic and notification delivery.

![Automation workflow](../../assets/screenshots/telegram/n8n_automation_alerts_workflow.png)

---

## Alert delivery — Telegram
Alerts are sent only when action is required.

![Telegram alert](../../assets/screenshots/telegram/telegram_energy_alert.png)

---

## Optional layer — Power BI native alerts
In addition to platform-level monitoring, Power BI KPI alerts can be used for threshold-based flags
(e.g., peak demand or off-hours consumption thresholds).

---

## Why this matters
- Prevents silent data failures
- Enables proactive operations
- Reduces manual dashboard checks
- Closes the loop: **data → insight → action**
