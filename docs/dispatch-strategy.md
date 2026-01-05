# Dispatch Strategy (v2)

This document describes the energy dispatch logic used in Smart Building EnergyOps (v2),
focusing on how PV, Battery (BESS), and Grid interact under hourly electricity prices.

## 1) Objective

**Primary objective:** minimize electricity cost (€)  
**Secondary constraints:** operational realism and system stability

This is a **decision-support simulation**, not a real-time EMS controller.

> Industry phrasing: *“cost-optimized dispatch”, “operational constraints”, “decision-support logic”.*

---

## 2) Priority Order (Energy Flow)

1. **PV-first self-consumption**
   - PV generation is used to serve on-site load first
   - Surplus PV can charge the battery or be exported

2. **Battery discharge (expensive hours)**
   - Battery discharges to reduce grid import when prices are high
   - SOC limits are always respected

3. **Grid import (last resort)**
   - Grid supplies remaining demand

> Industry phrasing: *“self-consumption priority”, “onsite coverage”.*

---

## 3) Charging Logic

Battery can charge from:
- **PV surplus** (always allowed)
- **Grid during cheap hours** (price-based condition)

Typical condition (example):
- charge from grid if `price_eur_per_kwh` is below a defined cheap threshold
- charging stops once SOC target is reached

> Industry phrasing: *“price-based charging”, “SOC target”.*

---

## 4) Discharge Logic

Battery discharges when:
- prices exceed a defined expensive threshold
- SOC is above minimum reserve

This represents **market arbitrage behavior**.

> Industry phrasing: *“arbitrage”, “price signal response”, “hysteresis”.*

---

## 5) Constraints & Safeguards

- SOC min / max enforced
- no simultaneous charge and discharge
- optional SOC reserve for peak shaving scenarios

> Industry phrasing: *“operational safeguards”, “hard constraints”.*

---

## 6) Outputs Written to Gold

Dispatch logic writes the following to the Gold fact table:
- `bess_charge_kwh`
- `bess_discharge_kwh`
- `bess_soc_pct`
- `grid_import_kwh`
- `grid_export_kwh`
- `cost_eur` (with dispatch)
- `cost_no_bess_eur` (baseline)

> Industry phrasing: *“baseline vs optimized scenario”.*

---

## 7) Validation Checks

After each run:
- battery both charges and discharges (non-zero counts)
- SOC remains within bounds
- total cost with BESS < cost without BESS

> Industry phrasing: *“behavioral validation”, “sanity checks”.*

