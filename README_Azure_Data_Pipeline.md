# 🚀 Azure Data Engineering Pipeline
### *End-to-End ETL Framework for Initial Load, Incremental Load & Backfill*

![Azure Architecture](a940aea0-be40-4b87-944f-79b4f92abfce.png)

---

## 🧩 Overview
This project demonstrates a **robust, parameterized, and reusable Azure Data Factory pipeline** designed to automate **Initial Loads**, **Incremental Loads**, and **Backfill operations**.

It’s built using **Azure’s modern data stack** — ensuring scalability, modularity, and end-to-end data lineage.
The solution is suitable for both **batch** and **near real-time** ingestion needs.

---

## 🏗️ Architecture Overview

### 🔹 End-to-End Flow
1. **Azure SQL DB (Source)** → Data extracted using **ADF Linked Service**
2. **Bronze Layer (Raw)** → Data stored in **Azure Data Lake Storage (ADLS)**
3. **Silver Layer (Transform)** → Cleaned & transformed in **Azure Databricks / Spark**
4. **Gold Layer (Curated)** → Modeled into **Delta Tables / Star Schema**
5. **Consumption Layer** → Queried via **Azure Synapse Analytics** or **Power BI**

![ADF Architecture Flow](6aeeef52-61b4-491c-8985-253b178b54a5.png)

---

## ⚙️ Key Features

| Feature | Description |
|----------|--------------|
| 🔁 **Initial Load** | Loads all historical data from source to target for the first time. |
| ⚡ **Incremental Load (CDC)** | Loads only new or modified data since last successful run. |
| 🧱 **Backfill Support** | Enables selective historical data reprocessing for a given date range. |
| 🧠 **Dynamic Pipeline** | Parameterized `ForEach` logic for multi-table ingestion. |
| 🚨 **Alert Mechanism** | Web Activity triggers real-time alerts on failure. |
| 🔒 **Secure Connections** | Managed identities and Key Vault integration for credentials. |
| 💡 **Reusability** | Modular design — extend to new datasets with minimal setup. |

---

## 🧰 Tech Stack

| Category | Technology |
|-----------|-------------|
| **Orchestration** | Azure Data Factory |
| **Storage** | Azure Data Lake (ADLS Gen2) |
| **Compute** | Azure Databricks, Apache Spark |
| **Database** | Azure SQL Database |
| **Data Modeling** | Delta Lake, Star Schema |
| **Visualization** | Power BI |
| **Version Control** | GitHub |
| **Alerting** | Webhook / REST API (Teams, Slack, etc.) |

![Tech Stack](88da0547-de28-4326-8b41-4edac9ffc27f.png)

---

## 🧮 Pipeline Logic

### 🧱 Components
- **last_cdc** — Retrieves the latest processed timestamp (checkpoint).
- **AzureSQLToLake** — Executes data extraction query using the CDC filter and loads to ADLS.
- **IfIncrementalData** — Conditional activity to decide between Initial or Incremental logic.
- **Web Alert** — Sends alert on pipeline failure to notify monitoring channels.

---

## ⚙️ Parameterization & Dynamic Execution

Each table ingestion is fully parameterized for flexibility:

| Parameter | Description |
|------------|-------------|
| `table_name` | Table to be ingested |
| `load_type` | `initial` / `incremental` / `backfill` |
| `cdc_column` | Timestamp column used for delta detection |
| `target_path` | Folder path in ADLS |
| `last_cdc` | Last processed timestamp (from metadata table) |

🧩 *This allows the same pipeline to dynamically process multiple tables in one execution.*

---

## 💻 Example ADF Expression

```json
@activity('last_cdc').output.resultsets[0].rows[0].cdc
```

Used to fetch the most recent CDC value for incremental loading.

---

## 🧰 Setup & Deployment

### 1️⃣ Clone Repository
```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
```

### 2️⃣ Import into Azure Data Factory
- Go to **Manage → ARM Template → Import Template**.
- Upload the JSON files from the repo.
- Create or link the following resources:
  - Azure SQL Database (Source)
  - ADLS Gen2 (Target)
  - Databricks (for transformation)
  - Key Vault (for secrets)

### 3️⃣ Configure Parameters
Update pipeline parameters with environment-specific values (connections, paths, etc.).

### 4️⃣ Trigger Pipeline
You can trigger manually or via REST API:
```bash
POST https://management.azure.com/subscriptions/{sub-id}/resourceGroups/{rg}/providers/Microsoft.DataFactory/factories/{factory}/pipelines/{pipeline}/createRun?api-version=2018-06-01
```

---

## 📊 Monitoring & Alerts

- **Success**: Status logged in ADF Monitor tab.
- **Failure**: Triggers **Web Activity** → sends JSON payload to your chosen alert endpoint (Teams, Slack, etc.).
- **Retries**: Configurable retry policies at activity level.

---

## 🗂️ Folder Structure

```
azure-data-pipeline/
│
├── pipelines/
│   ├── incremental_load.json
│   ├── initial_load.json
│   ├── backfill_pipeline.json
│
├── datasets/
│   ├── source_sql.json
│   ├── adls_target.json
│
├── linkedServices/
│   ├── AzureSQLDatabase.json
│   ├── AzureDataLake.json
│   ├── AzureDatabricks.json
│
├── notebooks/
│   ├── transformations/
│   │   ├── clean_and_enrich.py
│   │   ├── delta_merge_logic.py
│
└── README.md
```

---

## 🔮 Future Enhancements

- Integrate **Great Expectations** for data validation.
- Add **metadata-driven configuration** for all table mappings.
- Implement **real-time ingestion** using Event Grid + Stream Analytics.
- Add **Power BI / Synapse dashboard** for operational monitoring.

---

## 🏆 Results

✅ Reduced manual maintenance with parameterized ingestion logic.  
✅ Seamless switching between Initial, Incremental, and Backfill modes.  
✅ Automated alerting and monitoring.  
✅ Fully cloud-native and scalable design.

---

## 👨‍💻 Author

**Ankit Sharma**  
💼 *Data Engineer | Analytics & Automation Enthusiast*  
📍 *India*  
📧 [ankitsharma@example.com](mailto:ankitsharma@example.com)  
🔗 [LinkedIn](https://www.linkedin.com/in/ankit-sharma)

---

## 🌟 Repository Badges

![Azure Data Factory](https://img.shields.io/badge/Azure-Data%20Factory-blue?logo=microsoft-azure)
![Databricks](https://img.shields.io/badge/Azure-Databricks-orange?logo=databricks)
![Spark](https://img.shields.io/badge/Apache-Spark-red?logo=apache-spark)
![Python](https://img.shields.io/badge/Python-Scripting-yellow?logo=python)
![GitHub](https://img.shields.io/badge/VersionControl-GitHub-black?logo=github)
![Status](https://img.shields.io/badge/Status-Production%20Ready-success)
