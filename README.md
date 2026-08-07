# 🚀 Azure Databricks Incremental Pipeline

![Deploy to Databricks](https://github.com/Sonu7804/azure-databricks-incremental-pipeline/actions/workflows/deploy.yml/badge.svg)

A production-style incremental data pipeline built on Azure Databricks using Auto Loader, Delta Lake, GitHub Actions CI/CD, and Azure Key Vault for secure credential management.

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
| Auto Loader | Incremental file ingestion with checkpointing |
| Delta Lake | ACID-compliant storage format |
| Azure Data Lake Gen2 | Storage (Bronze/Silver/Gold) |
| Azure Data Factory | Pipeline orchestration & scheduling |
| Delta Live Tables | Declarative pipeline with data quality |
| Unity Catalog | Data governance & lineage |
| Azure Key Vault | Secure credential management |
| Power BI | Gold layer visualization |
| GitHub Actions | CI/CD — auto deploy notebooks |

---

## 🔐 Security — Azure Key Vault

All sensitive credentials are stored securely in Azure Key Vault — no hardcoded values anywhere in the codebase.

### How it works
1. Storage account key stored as secret in `sonu-kv-01` Key Vault
2. Databricks Secret Scope `kv-scope` linked to Key Vault
3. Notebooks fetch secrets at runtime using `dbutils.secrets.get()`
4. ADLS connected without any hardcoded credentials

```python
# Secure credential fetch — actual value never exposed in logs
storage_key = dbutils.secrets.get(scope="kv-scope", key="storage-account-key")
spark.conf.set(
    "fs.azure.account.key.sonudedatalake01.dfs.core.windows.net",
    storage_key
)
```

### RBAC Setup
| Role | Assigned To |
|------|------------|
| Key Vault Secrets Officer | Sonu Kushwaha (admin) |
| Key Vault Secrets User | AzureDatabricks (runtime) |

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

## 📁 Project Structure

```
├── .github/
│   └── workflows/
│       └── deploy.yml
├── screenshots/
├── autoloader_incremental_ingestion.ipynb
├── key_vault_integration.ipynb
└── README.md
```

---

## 🔑 Key Features

- **Incremental Ingestion** — Auto Loader with checkpointing, only new files processed
- **Schema Evolution** — Handles new columns automatically
- **Data Quality** — Delta Live Tables Expectations
- **Governance** — Unity Catalog three-level namespace
- **Secure Credentials** — Azure Key Vault, zero hardcoded values
- **Automated Deployment** — CI/CD via GitHub Actions

---

## 👤 Author

**Sonu Kushwaha**
- LinkedIn: [linkedin.com/in/sonu7804](https://linkedin.com/in/sonu7804)
- GitHub: [github.com/Sonu7804](https://github.com/Sonu7804)
