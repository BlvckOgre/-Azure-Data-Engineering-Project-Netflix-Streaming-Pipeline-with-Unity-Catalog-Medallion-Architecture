# 🔐 Unity Catalog Setup for Netflix Streaming Pipeline

This document outlines the setup, configuration, and governance principles used to implement Unity Catalog in the Netflix Azure Data Engineering Project.

## 🧭 Why Unity Catalog?

Unity Catalog provides centralized metadata management, fine-grained access control, and governance for data stored in Databricks. In this Netflix-style pipeline, Unity Catalog ensures:

- 🔒 Secure data access across layers (bronze, silver, gold)
- ✅ Schema validation and data lineage tracking
- 👥 Role-based access control (RBAC)
- 🧪 Auditing and compliance

## 🏗️ Unity Catalog Architecture

```
Unity Catalog
├── Catalog: netflix_catalog
│   ├── Schema: bronze_layer
│   │   └── Table: raw_netflix_events
│   ├── Schema: silver_layer
│   │   └── Table: cleaned_user_logs
│   ├── Schema: gold_layer
│   │   ├── Table: top_streamed_titles
│   │   └── Table: regional_engagement_metrics
```

## 📐 Setup Steps

### 1️⃣ Create the Catalog

```sql
CREATE CATALOG netflix_catalog COMMENT 'Netflix Streaming Project Catalog';
```

### 2️⃣ Create Schemas for Each Layer

```sql
CREATE SCHEMA netflix_catalog.bronze_layer COMMENT 'Raw streaming events from Event Hubs';
CREATE SCHEMA netflix_catalog.silver_layer COMMENT 'Cleaned and transformed data';
CREATE SCHEMA netflix_catalog.gold_layer COMMENT 'Aggregated business metrics';
```

### 3️⃣ Create Unity Catalog Tables

Tables are created in Databricks notebooks with `SAVEAS TABLE` syntax using Delta format.

```python
bronze_df.write.format("delta").saveAsTable("netflix_catalog.bronze_layer.raw_netflix_events")
```

Repeat for `silver_layer.cleaned_user_logs`, `gold_layer.top_streamed_titles`, etc.

### 4️⃣ Configure Access Control

Use SQL grants for fine-grained permissions.

```sql
GRANT USAGE ON CATALOG netflix_catalog TO `data_engineers`;
GRANT SELECT ON TABLE netflix_catalog.gold_layer.top_streamed_titles TO `analysts_group`;
```

### 5️⃣ Enable Data Lineage (Optional)

Lineage is tracked automatically if Unity Catalog and compute policies are correctly configured. Ensure you're using a Unity-enabled cluster.

## 🧑‍💼 Roles & Permissions Matrix

| Role             | Permissions                                       |
|------------------|---------------------------------------------------|
| `data_engineers` | Full access to bronze/silver layers               |
| `data_analysts`  | Read-only access to gold layer                    |
| `admins`         | Manage catalog, schemas, and grants               |

## 🔍 Governance Best Practices

- 📌 **Tag columns with PII metadata** where applicable.
- 🧪 **Enable audit logs** via Azure Monitor and Databricks logging.
- 🔁 **Use versioned schemas** to handle evolving datasets.
- 🧰 **Leverage workspace bindings** for secure multi-tenant architecture.

## 📎 Resources

- [Databricks Unity Catalog Documentation](https://docs.databricks.com/data-governance/unity-catalog/index.html)
- [Delta Lake Table Properties](https://docs.delta.io/latest/delta-table-properties.html)

---
This Unity Catalog configuration ensures compliance, auditability, and security for streaming data pipelines that scale with enterprise needs.