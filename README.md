# 🚀 Azure Databricks Incremental Pipeline

![Deploy to Databricks](https://github.com/Sonu7804/azure-databricks-incremental-pipeline/actions/workflows/deploy.yml/badge.svg)

A production-style incremental data pipeline built on Azure Databricks using Auto Loader, Delta Lake, and GitHub Actions CI/CD.

---

## 🏗️ Architecture

**Medallion Architecture** — Bronze → Silver → Gold

- **Bronze**: Raw data ingested incrementally using Databricks Auto Loader
- **Silver**: Cleaned and transformed data using PySpark
- **Gold**: Aggregated, business-ready data for analytics

---

## ⚙️ Tech Stack

| Tool | Purpose |
|------|---------|
| Azure Databricks | Compute & Notebooks |
| Auto Loader | Incremental file ingestion |
| Delta Lake | ACID-compliant storage format |
| Azure Data Lake Gen2 | Storage (Bronze/Silver/Gold) |
| Azure Data Factory | Pipeline orchestration & scheduling |
| Delta Live Tables | Declarative pipeline with data quality |
| Unity Catalog | Data governance & lineage |
| Power BI | Gold layer visualization |
| GitHub Actions | CI/CD — auto deploy notebooks |

---

## 🔄 CI/CD Pipeline

Automated deployment using **GitHub Actions**.

Every push to `main` branch automatically deploys the latest notebook to Databricks workspace.

### How it works
1. Code pushed to `main` branch
2. GitHub Actions triggers `deploy.yml` workflow
3. Databricks CLI authenticates using secrets (`DATABRICKS_HOST`, `DATABRICKS_TOKEN`)
4. Notebook deployed to `/Workspace/Users/sonu.kushwaha1@studentambassadors.com/`

### Secrets Required
| Secret | Description |
|--------|-------------|
| `DATABRICKS_HOST` | Databricks workspace URL |
| `DATABRICKS_TOKEN` | Personal Access Token |
---

## 🔑 Key Features

- **Incremental Ingestion** — Auto Loader with checkpointing, only new files processed
- **Schema Evolution** — Handles new columns automatically
- **Data Quality** — Delta Live Tables Expectations
- **Governance** — Unity Catalog three-level namespace
- **Automated Deployment** — CI/CD via GitHub Actions

---

## 👤 Author

**Sonu Kushwaha**
- LinkedIn: [linkedin.com/in/sonu7804](https://linkedin.com/in/sonu7804)
- GitHub: [github.com/Sonu7804](https://github.com/Sonu7804)

---

## 📁 Project Structure
