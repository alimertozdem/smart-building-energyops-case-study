# 03 — Landing (Azure Blob / OneLake)

## Goal
Store ingested datasets in a partitioned, analytics-friendly
landing zone that supports incremental processing.

---

## Landing structure
All datasets are written to Azure Blob Storage
(using OneLake-compatible paths).

Each domain follows the same structure:


---

## Example — Energy (monthly CSV)

Below is an example of a single monthly export
for energy consumption.

- Exactly **one CSV per month**
- File naming includes building_id and period
- Optimized for downstream lakehouse ingestion

![Azure landing partition](../../assets/screenshots/azure/azure_landing_energy_month_partition.png)

---

## Design decisions
- Monthly partitioning instead of daily:
  - Fewer files
  - Faster metadata operations
- Explicit `building_id / year / month` folders:
  - Partition pruning
  - Multi-building scalability
- CSV format:
  - Transparent
  - Easy to debug
  - Fabric-friendly
