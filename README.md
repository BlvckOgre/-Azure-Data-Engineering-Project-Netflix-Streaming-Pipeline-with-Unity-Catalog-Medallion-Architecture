
# 🎬 Azure Data Engineering Project – Netflix Streaming Pipeline with Unity Catalog & Medallion Architecture

## 📘 Overview

This repository contains an end-to-end real-time Azure Data Engineering project built around Netflix-style streaming data, simulating user behavior and viewing logs. The project demonstrates how to design and implement a scalable, governed, and modular data pipeline using Azure Databricks, Unity Catalog, Delta Lake, and Medallion Architecture.

> **Scenario**: You're tasked with building a production-grade data engineering pipeline for a company like Netflix to handle streaming user interactions such as plays, pauses, searches, and recommendations.



## 🎯 Project Objectives

- Build a real-time ingestion and transformation pipeline for Netflix-style data.
- Implement the Medallion Architecture to model raw to refined data flows.
- Use Unity Catalog to manage data governance, access control, and schema evolution.
- Demonstrate best practices in streaming ETL, data security, and lakehouse design.
- Simulate real-time decision-making by processing high-velocity event data.

## 🧠 Project Design & Data Engineering Thinking

### 🔁 Real-Time Data Ingestion

- Simulates Netflix user actions streaming into the system via Azure Event Hubs.
- Consumes this data using Structured Streaming in Databricks (Kafka-compatible).

### 🏛️ Medallion Architecture

| Layer    | Description |
|----------|-------------|
| **Bronze** | Ingested raw data from Netflix-like user streams (immutable, unparsed). |
| **Silver** | Cleaned, parsed, and validated logs, e.g., valid timestamps, structured fields. |
| **Gold** | Business-ready metrics: user behavior summaries, engagement scores, regional trends. |

![Medallion Architecture](Medallion%20Architecture/NetflixStructure.PNG)
### 🔐 Unity Catalog

- Manages access policies, lineage, data ownership, and schema consistency across layers.
- Supports multi-workspace governance for secure, enterprise-scale operations.

### 🏠 Delta Lakehouse

- Delta format enables ACID transactions, schema evolution, and time travel across layers.
- Forms the foundation for downstream analytics and machine learning workflows.

## 🧰 Tools & Technologies

| Category | Tools / Services |
|----------|------------------|
| Cloud Platform | Microsoft Azure |
| Stream Ingestion | Azure Event Hubs |
| Data Processing | Azure Databricks (PySpark, Delta Lake) |
| Storage | Azure Data Lake Storage Gen2 (ADLS) |
| Data Governance | Unity Catalog |
| Workflow Orchestration | Azure Data Factory (ADF) |
| Security | Azure Key Vault |
| Structured Storage | Azure SQL Database |
| Monitoring | Azure Monitor, Databricks logs |
| Version Control | Git + GitHub |

## 🧑‍💻 Skills Required / Developed

- Cloud Data Engineering (Azure)
- PySpark & SQL Programming
- Streaming Pipeline Design (Structured Streaming)
- Delta Lake / Lakehouse Architecture
- Medallion Architecture Principles
- Data Governance (Unity Catalog)
- Key Vault and Secure Secret Management
- ETL/ELT Orchestration (ADF)
- Problem Solving & Debugging distributed systems

## 🗺️ Project Structure

```
netflix-streaming-pipeline/
├── notebooks/
│   ├── 01_ingest_bronze_streaming.py
│   ├── 02_transform_silver_cleaning.py
│   └── 03_aggregate_gold_enrichment.py
├── adf_pipelines/
│   ├── ingest_pipeline.json
│   └── trigger_config.json
├── data_schema/
│   └── netflix_eventhub_schema.json
├── configs/
│   ├── keyvault_config.json
│   └── storage_paths.json
├── documentation/
│   └── unity_catalog_setup.md
├── README.md
└── LICENSE
```

## 🔍 Netflix Pipeline Walkthrough: Step-by-Step

### 1️⃣ Ingest Netflix Event Stream (Bronze)
- Simulated user events (e.g., `play`, `pause`, `search`) sent to Event Hubs.
- Databricks reads streaming data and writes it to ADLS in Delta format (raw, unstructured).

### 2️⃣ Clean and Parse Data (Silver)
- Remove corrupt records, convert timestamp formats, and apply transformations.
- Extract relevant fields such as `user_id`, `title`, `action_type`, `device_type`.

### 3️⃣ Aggregate Business Metrics (Gold)
- Calculate metrics like:
  - Most streamed shows by region
  - Average session duration
  - Peak traffic hours
- Store clean data for Power BI dashboards or ML pipelines.

### 4️⃣ Unity Catalog Setup
- Created secure schemas (catalogs) for each layer.
- Configured roles and row-level access policies.
- Ensured lineage tracking and schema validation.

### 5️⃣ Orchestrate with Azure Data Factory
- Built ADF pipeline that:
  - Triggers notebook workflows
  - Pulls secrets from Key Vault
  - Logs success/failure for observability

## 📝 Key Concepts Summary

| Concept | Description |
|--------|-------------|
| Medallion Arch. | Layered architecture that enforces data quality and transformation standards |
| Delta Lake | Storage layer with ACID transactions and performance optimization |
| Unity Catalog | Databricks-native governance for multi-user, multi-workspace control |
| Event Hubs | Real-time ingestion service used for Netflix-style event simulation |
| Structured Streaming | Continuous data processing API in PySpark |
| Lakehouse | Combines the best of data lakes and data warehouses in one architecture |

## 📈 Expected Outcomes

- ✅ Real-time Netflix-style data ingestion and transformation
- ✅ Medallion-based architecture with Delta Lake
- ✅ Secure governance using Unity Catalog and Azure Key Vault
- ✅ Reusable, modular ADF pipeline for orchestration
- ✅ Foundation for real-time analytics and user behavior modeling

## 💡 Recommendations & Lessons

- **Build Unity Catalog early**: Ensures schemas and permissions are properly designed.
- **Stream with Delta Live Tables**: Adds robustness to streaming workloads.
- **Audit everything**: Monitor job status, log metrics, and set alerts for production systems.
- **Partition wisely**: By time or region for large-scale streaming datasets.

## 📩 Get in Touch

**Author**: Dimakatso Malope
**LinkedIn**: [Your LinkedIn Profile]  
**Email**: [Your Email]

---
