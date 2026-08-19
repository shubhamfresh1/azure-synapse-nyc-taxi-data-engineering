# 🚕 Azure Synapse NYC Taxi Data Engineering Project

## 📌 Project Overview

This project demonstrates an end-to-end **data engineering solution for New York City Green Taxi trip data using Microsoft Azure Synapse Analytics and Azure Data Lake Storage Gen2**.

The project covers the complete data lifecycle from raw data exploration and external data access through **Bronze, Silver, and Gold data layers**, data cleansing, quality validation, joins, stored procedures, views, aggregations, and analytical datasets.

The implementation combines **Synapse Serverless SQL and Apache Spark** to demonstrate practical cloud data engineering patterns.

---

## 🎯 Project Objectives

The primary objectives of this project are to:

* Store and process NYC Taxi data in Azure Data Lake Storage Gen2.
* Explore raw CSV, Parquet, and Delta-format data.
* Query files using Synapse Serverless SQL.
* Create external data sources and external file formats.
* Build Bronze-layer external tables/views.
* Transform and cleanse data into Silver-layer datasets.
* Create reusable stored procedures for transformations.
* Perform joins between fact and reference datasets.
* Implement data-quality and duplicate checks.
* Create Gold-layer analytical datasets and views.
* Perform aggregations for analytical use cases.
* Use Synapse Spark for distributed data processing.

---

# 🏗️ Architecture

```text
                    NYC GREEN TAXI DATA
                             │
                             ▼
                  Azure Data Lake Storage Gen2
                             │
              ┌──────────────┴──────────────┐
              │                             │
              ▼                             ▼
       CSV / Parquet / Delta          Reference Data
              │                             │
              └──────────────┬──────────────┘
                             ▼
                 Azure Synapse Analytics
                             │
              ┌──────────────┴──────────────┐
              │                             │
              ▼                             ▼
        Serverless SQL                Synapse Spark
              │                             │
              ▼                             ▼
        🥉 BRONZE LAYER              Spark Processing
              │
              ▼
        🥈 SILVER LAYER
              │
       ┌──────┼────────┐
       │      │        │
       ▼      ▼        ▼
    Cleansing Joins  Data Quality
       │      │        │
       └──────┼────────┘
              ▼
         🥇 GOLD LAYER
              │
              ▼
       Views / Aggregations
              │
              ▼
       Analytical Datasets
```

---

# ☁️ Azure Architecture Components

| Component                    | Purpose                                      |
| ---------------------------- | -------------------------------------------- |
| Azure Data Lake Storage Gen2 | Stores raw and processed data                |
| Azure Synapse Analytics      | Cloud analytics and data processing          |
| Synapse Serverless SQL       | Queries data directly from the data lake     |
| Synapse Spark                | Distributed data processing                  |
| Synapse SQL Scripts          | Data definition, transformation and analysis |
| Synapse Pipelines            | Orchestrates processing activities           |
| Synapse Datasets             | Defines data inputs and outputs              |
| Linked Services              | Provides connections to data sources         |
| Integration Runtime          | Supports data integration activities         |
| Triggers                     | Supports pipeline execution                  |

---

# 📂 Data Sources

The project works primarily with **NYC Green Taxi trip data** and supporting reference datasets.

The repository includes exploration and processing scripts for:

* Green Taxi trip data
* Taxi zone data
* Calendar data
* Vendor information
* Payment type
* Rate code
* Trip type
* Reference/lookup data

The original large datasets are **not stored in this repository**.

---

# 🔄 Data Engineering Workflow

## 1. Raw Data Exploration

The first stage focuses on understanding the source data.

The SQL scripts include exploration of:

* Taxi zones
* Calendar attributes
* Vendor information
* Payment types
* Rate codes
* Green Taxi CSV data
* Green Taxi Parquet data
* Green Taxi Delta data

This establishes an understanding of the raw schema and available attributes before transformation.

---

# 🥉 Bronze Layer

The Bronze layer represents the raw data with minimal transformation.

The project creates:

* External data sources
* External file formats
* External Bronze tables
* Bronze views

This allows Synapse Serverless SQL to query data stored in ADLS Gen2 without requiring the complete dataset to be loaded into a traditional relational table.

### Bronze workflow

```text
Raw Files in ADLS Gen2
        │
        ▼
External Data Source
        │
        ▼
External File Format
        │
        ▼
Bronze External Tables
        │
        ▼
Bronze Views
```

---

# 🥈 Silver Layer

The Silver layer contains cleansed, standardized and transformed datasets.

The project creates Silver objects for:

* Green Taxi trip data
* Taxi zones
* Calendar
* Vendor
* Payment type
* Trip type
* Rate code

Transformation logic includes:

* Data cleansing
* Data type handling
* Filtering
* Joining
* Standardization
* Derived attributes
* Data-quality validation

---

# 🧹 Data Quality

Data quality is an important part of the project.

The SQL implementation includes dedicated scripts for:

* Duplicate detection
* Data-quality checks
* Invalid records
* Missing or unexpected values
* Validation of transformed data

Example:

```sql
-- Example data-quality validation

SELECT
    COUNT(*) AS invalid_records
FROM silver_trip_data
WHERE trip_distance <= 0;
```

The exact validation rules depend on the source dataset and transformation requirements.

---

# 🔗 Data Integration and Joins

Reference datasets are joined with the main Green Taxi trip data to enrich the analytical dataset.

Examples include relationships between:

```text
Green Taxi Trips
       │
       ├── Taxi Zone
       ├── Calendar
       ├── Vendor
       ├── Payment Type
       ├── Trip Type
       └── Rate Code
```

This produces a more useful analytical model than relying on the raw trip data alone.

---

# 🥇 Gold Layer

The Gold layer contains analytics-ready datasets and views.

The project creates Gold objects for Green Taxi data and includes:

* Gold trip data
* Gold views
* Aggregated trip datasets
* Analytical queries

The Gold layer is designed for downstream analytics and reporting.

---

# ⚙️ Stored Procedures

The project uses stored procedures to encapsulate transformation logic.

Stored procedures are implemented for operations including:

* Silver trip-data creation
* Taxi-zone processing
* Calendar processing
* Trip-type processing
* Vendor processing
* Payment-type processing
* Rate-code processing
* Gold trip-data creation

This demonstrates reusable SQL transformation logic rather than placing all processing into one large script.

---

# 📊 CTAS and Aggregation

The project also demonstrates **CTAS — CREATE TABLE AS SELECT** for creating analytical datasets from transformed data.

Example use case:

```text
Silver Trip Data
       │
       ▼
Aggregation
       │
       ▼
CTAS
       │
       ▼
Gold Analytical Dataset
```

This approach is useful for creating optimized analytical structures from transformed data.

---

# ⚡ Apache Spark

The project also contains a Synapse Spark notebook for creating an aggregated Gold dataset.

The notebook demonstrates how Spark can be used alongside Synapse SQL for distributed data processing.

```text
NYC Taxi Data
      │
      ▼
Synapse Spark
      │
      ▼
Distributed Processing
      │
      ▼
Aggregated Dataset
```

---

# 🔄 Synapse Pipelines

The repository contains Synapse pipelines that orchestrate different stages of the transformation process.

Key pipelines include:

```text
pl_execute_all_pipeline
        │
        ├── pl_create_silver_tables
        ├── pl_create_silver_taxi_zone
        ├── pl_create_silver_taxi_zone_usp
        ├── pl_create_silver_trip_data_green
        ├── pl_create_gold_trip_data_green
        └── pl_create_gold_trip_data_agg
```

These pipelines demonstrate orchestration of the data-engineering workflow inside Azure Synapse.

---

# 🧩 Synapse SQL Implementation

The repository contains SQL scripts covering the complete transformation lifecycle.

### Database and External Objects

```text
1_create_databases
2_create_external_data_sources
3_create_external_file_format
4_create_external_bronze_tables
5_create_bronze_view
```

### Data Exploration

```text
SQL taxi zone exploration
Calendar exploration
Vendor exploration
Payment type exploration
Rate code exploration
Green Taxi CSV exploration
Green Taxi Parquet exploration
Green Taxi Delta exploration
```

### Silver Layer

```text
Silver Taxi Zone
Silver Calendar
Silver Trip Type
Silver Rate Code
Silver Vendor
Silver Payment Type
Silver Trip Data
```

### Data Quality

```text
Duplicate detection
Data-quality checks
File joining
```

### Gold Layer

```text
Gold Trip Data
Gold Views
Gold Aggregations
CTAS analytical datasets
```

The repository currently contains a substantial collection of these SQL scripts.

---

# 📁 Repository Structure

```text
azure-synapse-nyc-taxi-data-engineering/
│
├── credential/
│
├── dataset/
│
├── integrationRuntime/
│
├── linkedService/
│
├── notebook/
│   └── 1_spark_create_gold_trip_data_green_agg.json
│
├── pipeline/
│   ├── pl_create_gold_trip_data_agg.json
│   ├── pl_create_gold_trip_data_green_.json
│   ├── pl_create_silver_tables.json
│   ├── pl_create_silver_taxi_zone.json
│   ├── pl_create_silver_taxi_zone_usp.json
│   ├── pl_create_silver_trip_data_green.json
│   └── pl_execute_all_pipeline.json
│
├── sqlscript/
│   ├── Database setup
│   ├── External data sources
│   ├── External file formats
│   ├── Bronze objects
│   ├── Silver transformations
│   ├── Stored procedures
│   ├── Data-quality checks
│   ├── Joins
│   ├── Gold objects
│   └── Analytical queries
│
├── trigger/
│
├── README.md
│
└── publish_config.json
```

The current repository contains these Synapse artifact categories at the root, including datasets, integration runtime, linked services, notebooks, pipelines, SQL scripts, triggers and configuration files.

---

# 🛠️ Technologies Used

* Microsoft Azure
* Azure Synapse Analytics
* Azure Data Lake Storage Gen2
* Synapse Serverless SQL
* Apache Spark
* PySpark / Spark notebooks
* T-SQL
* SQL Stored Procedures
* CTAS
* External Tables
* External Data Sources
* External File Formats
* Git
* GitHub

---

# 📚 Key Data Engineering Concepts Demonstrated

This project demonstrates practical knowledge of:

* Cloud data lakes
* Azure Synapse Analytics
* Serverless SQL
* External tables
* External data sources
* External file formats
* Bronze-Silver-Gold architecture
* Data transformation
* Data cleansing
* Data-quality validation
* Duplicate detection
* SQL joins
* Stored procedures
* CTAS
* Analytical aggregations
* Views
* Spark processing
* Pipeline orchestration
* Data modeling
* Reference/lookup data integration

---

# 📈 Analytical Use Cases

The transformed NYC Taxi data can support analysis such as:

* Trip volume
* Trip distance
* Passenger behavior
* Fare and revenue analysis
* Payment-method distribution
* Vendor analysis
* Trip-type analysis
* Taxi-zone analysis
* Time-based trip patterns
* Aggregated trip metrics

---

# 🚀 How to Reproduce

## Prerequisites

You need:

* Azure subscription
* Azure Synapse Analytics workspace
* ADLS Gen2 storage account
* NYC Green Taxi dataset
* Synapse Serverless SQL access
* Synapse Spark capability if running the Spark notebook

## High-Level Setup

1. Create an ADLS Gen2 storage account.
2. Upload the NYC Green Taxi source files.
3. Create an Azure Synapse Analytics workspace.
4. Configure the required Linked Services.
5. Configure datasets and storage paths.
6. Configure the Synapse SQL environment.
7. Create the external data sources.
8. Create the external file formats.
9. Create Bronze-layer objects.
10. Execute Silver-layer transformation scripts.
11. Run data-quality checks.
12. Execute the Gold-layer transformations.
13. Run the analytical aggregation.
14. Execute the Synapse pipelines.
15. Run the Spark notebook where required.
16. Validate the final analytical datasets.

---

# 🔐 Security

This repository is intended to contain **code and Synapse project artifacts, not secrets**.

Never commit:

* Azure access keys
* Storage account keys
* SAS tokens
* Passwords
* Client secrets
* Connection strings containing credentials
* Authentication tokens

Use placeholders or secure Azure configuration mechanisms instead.

> Before publishing or sharing the repository, verify that the `credential/` directory and configuration files contain no active secrets.

---

# 🔮 Future Improvements

Potential improvements include:

* Azure Data Factory orchestration
* Incremental data loading
* Automated data-quality framework
* Metadata-driven pipelines
* Power BI reporting layer
* CI/CD using GitHub Actions or Azure DevOps
* Infrastructure as Code
* Monitoring and alerting
* Performance optimization
* Partitioning strategies
* Additional Spark transformations
* Production-style parameterization

---

# 👨‍💻 Author

## Shubham Jamdhade

** Azure Data Engineer**

### Core Skills

`Python` · `SQL` · `PySpark` · `Azure Data Factory` · `Azure Databricks` · `ADLS Gen2` · `Delta Lake` · `Azure Synapse Analytics`

---

## ⭐ Project Highlights

This project demonstrates how a raw cloud-based dataset can be transformed into structured, analytics-ready data using Azure Synapse.

```text
RAW DATA
   ↓
ADLS Gen2
   ↓
BRONZE
   ↓
SILVER
   ↓
DATA QUALITY + JOINS
   ↓
GOLD
   ↓
AGGREGATIONS
   ↓
ANALYTICS
```

⭐ If you find this project useful, feel free to star the repository.
