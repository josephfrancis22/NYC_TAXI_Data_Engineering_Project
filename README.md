# NYC_TAXI_Data_Engineering_Project
# NYC Taxi — Azure End-to-End Data Engineering Project

An end-to-end data engineering pipeline built on Azure that ingests NYC Taxi trip data via API, transforms it using PySpark in Databricks, stores it across Bronze, Silver, and Gold layers in ADLS Gen2, and serves it to Power BI through Delta tables.



---

## Tech Stack

- **Azure Data Factory** — dynamic parameterized data ingestion via HTTP API
- **Azure Data Lake Storage Gen2** — layered storage (Bronze / Silver / Gold)
- **Azure Databricks** — PySpark transformations and Delta table management
- **Delta Lake** — ACID transactions, versioning, and time travel
- **Power BI** — reporting and visualization
- **Security** — Azure AD Service Principal with Storage Blob Data Contributor role

---

## Project Phases

### Phase 1 — Ingestion (Azure Data Factory)
- Pulls Green Taxi trip Parquet files directly from the NYC TLC website via HTTP API
- Uses a **ForEach loop** with a parameterized dataset to dynamically download all 12 monthly files
- Includes an **IF condition** to handle leading zeros for months 01–09 vs 10–12
- Stores raw files in the **Bronze** container of ADLS Gen2

### Phase 2 — Transformation (PySpark / Silver Layer)
- Reads raw Parquet files from Bronze using Spark with a custom DDL schema
- Applies transformations: column renaming, split functions, date extractions (`year`, `month`, `to_date`)
- Writes cleaned data to the **Silver** container in Parquet format

### Phase 3 — Gold Layer & Delta Lake
- Reads Silver data and writes it to the **Gold** container in Delta format
- Registers Delta tables in a Databricks database for Spark SQL access
- Demonstrates Delta Lake features: versioning, `DESCRIBE HISTORY`, time travel (`VERSION AS OF`), and `RESTORE TABLE`

### Reporting
- Connects Gold layer Delta tables to **Power BI Desktop** via Databricks Partner Connect and access token

---

## Dataset

**Source:** [NYC TLC Trip Record Data](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)

- Green Taxi trip records — 2023 (12 monthly Parquet files via API)
- `trip_type.csv` — lookup file (manually uploaded to Bronze)
- `taxi_zone_lookup.csv` — zone/borough lookup (manually uploaded to Bronze)

---

## Prerequisites

- Azure free account (or pay-as-you-go)
- Azure Data Factory instance
- Azure Databricks workspace (Premium tier)
- Azure Data Lake Storage Gen2 account with containers: `bronze`, `silver`, `gold`
- Power BI Desktop

---


## Author

**Joseph Francis**
GitHub: [@josephfrancis22](https://github.com/josephfrancis22)

