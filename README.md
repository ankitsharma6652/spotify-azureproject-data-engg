# 🚀 Spotify Azure Data Engineering Pipeline  
### *End-to-End ETL Solution for Initial, Incremental, and Backfill Loads*




---

## 🧩 Overview  
This project demonstrates a **robust and automated data pipeline** built in **Azure Data Factory (ADF)** to handle **Initial Load**, **Incremental Load**, and **Backfill operations** efficiently.  

It integrates multiple Azure components — **SQL Database, Data Lake, Databricks, and Synapse Analytics** — to build a scalable and production-ready **ETL framework** that supports both **real-time and batch** processing.

---

## ⚙️ Key Features  

✅ **Initial Load** — Loads the complete dataset from the source system into the Data Lake for the first time.  
✅ **Incremental Load** — Loads only new or updated records using CDC logic and last modified timestamps.  
✅ **Backfill Support** — Enables historical data loading for specific time periods when needed.  
✅ **Dynamic ForEach Logic** — Parameterized looping for multiple table ingestion.  
✅ **Error Handling & Alerts** — Webhook-based failure alerts (e.g., Slack, Teams, Email).  
✅ **Modular & Scalable Design** — Easily extensible for additional sources and destinations.  

---

## 🏗️ Architecture  

The pipeline follows a **multi-layer architecture** to ensure clean data flow and reusability.

### 🔹 Data Flow  
1. **Source Systems (SQL / APIs / Files)**  
   → Extracted using **ADF Linked Services**.  
2. **Raw Layer (Bronze)**  
   → Initial/Incremental load written to **Azure Data Lake Storage (ADLS)**.  
3. **Transform Layer (Silver)**  
   → Processed using **Azure Databricks + Spark** for cleaning and enrichment.  
4. **Semantic Layer (Gold)**  
   → Modeled into **Delta Tables** or **Star Schema** for reporting.  
5. **Consumption Layer**  
   → Exposed to **Synapse / Power BI / Tableau** for analytics and visualization.

<img width="1408" height="736" alt="image" src="https://github.com/user-attachments/assets/f5c2898b-4e0f-4347-b1e0-c622545cf04e" />
---

## 🧠 Tech Stack  

| Component | Technology |
|------------|-------------|
| **Orchestration** | Azure Data Factory |
| **Storage** | Azure Data Lake |
| **Compute/Transform** | Azure Databricks, Apache Spark |
| **Database** | Azure SQL |
| **Version Control** | GitHub |
| **Visualization** | Power BI |
| **Notification** | Web Activity (REST API) |

<img width="1687" height="945" alt="image" src="https://github.com/user-attachments/assets/19db39c9-7a9e-423d-8c3d-2106ebd1f900" />


---

## 🔄 Pipeline Design  

### 🧱 Components  
- **last_cdc** → Retrieves last processed timestamp.  
- **AzureSQLToLake** → Extracts data from SQL and stores it in ADLS.  
- **IfIncrementalData** → Decides load type (Initial vs Incremental).  
- **Web Activity** → Triggers failure alerts when errors occur.  

<img width="1040" height="447" alt="image" src="https://github.com/user-attachments/assets/8af1ef66-9e20-4b4c-a497-d3ad0d8f22f2" />


---

## 🧮 Parameterization  

The pipeline is fully parameterized:  
- **Table Name**  
- **Load Type** (Initial / Incremental / Backfill)  
- **CDC Column**  
- **Target Path**  
- **Last Processed Timestamp**

This allows running the same pipeline dynamically for multiple tables and load types.

---

## 🧰 Setup Instructions  

1. **Clone Repository**  
   ```bash
   git@github.com:ankitsharma6652/spotify-azureproject-data-engg.git
   cd spotify-azureproject-data-engg.git
   ```

2. **Deploy to Azure Data Factory**  
   - Import ARM template or create pipeline manually using JSON.  
   - Configure Linked Services (SQL, Data Lake, Databricks).  

3. **Configure Parameters**  
   - Update connection strings and dataset parameters.  

4. **Trigger Pipeline**  
   - Run via ADF UI or programmatically using REST API.  

---

## 🚨 Error Handling & Alerts  

- On failure, pipeline sends alerts through **Web Activity** (e.g., Teams/Slack webhook).  
- Errors are logged with full activity run IDs for debugging.  

---

## 📈 Future Enhancements  

- Add **data quality checks** using Great Expectations.  
- Implement **metadata-driven framework** for table configuration.  
- Integrate **Azure Event Grid** for real-time triggering.  

---

## 👨‍💻 Author  

**Ankit Sharma**  
Data Engineer | Analytics Enthusiast  
💼 [LinkedIn](https://www.linkedin.com/in/ankit-sharma)  
📧 [Email](mailto:ankitcoolji@gmail.com)
