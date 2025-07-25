Walmart Sales Data Ingestion into BigQuery (Industrial Project)
This project demonstrates a real-time ETL pipeline using Apache Airflow to ingest Walmart sales data from Google Cloud Storage (GCS) into Google BigQuery. The pipeline handles data ingestion, staging, transformation, and loading into a target fact table using a MERGE operation.

🛠️ Tech Stack
Python

Apache Airflow

Google Cloud Storage (GCS)

Google BigQuery

BigQuery Operators & GCSToBigQueryOperator

🧩 Pipeline Architecture
pgsql
Copy
Edit
GCS (Raw JSON Files)
     ↓
Airflow DAG
     ↓
BigQuery (Staging & Dim Tables)
     ↓
BigQuery MERGE (Upsert into Fact Table)
📁 Folder Structure
bash
Copy
Edit
.
├── dags/
│   └── walmart_sales_etl_gcs.py        # Main Airflow DAG script
├── data/
│   ├── walmart-merchant/*.json         # Merchant data in JSON format
│   └── walmart-sales/*.json            # Sales data in JSON format
└── README.md                           # Project documentation
🚀 DAG Workflow Breakdown
Create BigQuery Dataset

Creates walmart_dwh dataset in BigQuery if it doesn't exist.

Create Tables

merchants_tb (dimension table)

walmart_sales_stage (staging table)

walmart_sales_tgt (target fact table)

Ingest Data from GCS to BigQuery

Uses GCSToBigQueryOperator to load merchant and sales data from GCS into their respective tables.

Upsert into Fact Table

Uses BigQueryInsertJobOperator to run a MERGE query to update or insert records from staging into the target table.

💡 Key Features
Dynamic creation of datasets and tables using Airflow operators

Parallel loading of dimension and staging data

Efficient upsert logic using BigQuery MERGE

Modular and production-ready DAG design

🔁 Schedule
DAG Interval: Runs daily (@daily)

Catchup: Disabled (to avoid backfills)

📌 Notes
GCS bucket name: walmart-ingestions

Data format: NEWLINE_DELIMITED_JSON

GCP Project: grounded-region-463501-n1

Dataset: walmart_dwh

✅ Prerequisites
GCP Project with access to BigQuery and GCS

Airflow environment with apache-airflow-providers-google installed

Service account with proper IAM permissions

🧪 Sample Airflow Command to Trigger DAG
bash
Copy
Edit
airflow dags trigger walmart_sales_etl_gcs
📷 Visualization
You can visualize the DAG and monitor task status through the Airflow web UI:

csharp
Copy
Edit
create_dataset
      ↓
[create_merchants_table, create_walmart_sales_table, create_target_table]
      ↓
     load_data
      ↓
merge_walmart_sales
👨‍💻 Author
Raushan Kumar
Cloud Data Engineer | GCP | BigQuery | Airflow
