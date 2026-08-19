# azure-synapse-nyc-taxi-data-engineering
# 🚕 Azure Synapse NYC Taxi Data Engineering Project

![Azure](https://img.shields.io/badge/Azure-Synapse%20Analytics-0078D4)
![SQL](https://img.shields.io/badge/SQL-T--SQL-blue)
![PySpark](https://img.shields.io/badge/PySpark-Apache%20Spark-orange)
![ADLS Gen2](https://img.shields.io/badge/Storage-ADLS%20Gen2-0078D4)
![Data Engineering](https://img.shields.io/badge/Focus-Data%20Engineering-green)

## 📌 Project Overview

This project demonstrates an end-to-end data engineering workflow for analyzing **New York City Taxi trip data using Microsoft Azure Synapse Analytics**.

The project focuses on ingesting, exploring, transforming, and analyzing taxi trip data using Azure cloud data services and SQL-based analytics.

The solution demonstrates practical concepts including:

* Azure Synapse Analytics
* Azure Data Lake Storage Gen2
* Serverless SQL
* Apache Spark / PySpark
* SQL-based data analysis
* Data transformation
* Data quality validation
* Cloud data architecture

---

## 🎯 Project Objectives

The main objectives of this project are to:

1. Store NYC Taxi data in Azure Data Lake Storage Gen2.
2. Connect Azure Synapse Analytics to the data lake.
3. Explore raw data using Synapse SQL.
4. Perform data transformations and cleansing.
5. Analyze taxi trips using SQL and Spark.
6. Generate business-oriented analytical insights.
7. Demonstrate an Azure-based data engineering architecture.

---

## 🏗️ Architecture

```text
                    NYC TAXI DATA
                          │
                          ▼
                Azure Data Lake Storage Gen2
                          │
                          ▼
                Azure Synapse Analytics
                          │
             ┌────────────┴────────────┐
             │                         │
             ▼                         ▼
       Serverless SQL             Apache Spark
             │                         │
             ▼                         ▼
       Data Exploration          Transformation
             │                         │
             └────────────┬────────────┘
                          ▼
                   Curated Dataset
                          │
                          ▼
                    SQL Analytics
                          │
                          ▼
                    Data Insights
```

> The architecture diagram above represents the main logical flow of the project. Implementation details may vary depending on the Synapse components used.

---

## 🛠️ Technologies Used

| Technology                   | Purpose                           |
| ---------------------------- | --------------------------------- |
| Microsoft Azure              | Cloud platform                    |
| Azure Synapse Analytics      | Analytics and data processing     |
| Azure Data Lake Storage Gen2 | Data storage                      |
| Serverless SQL               | Querying data in the data lake    |
| Apache Spark                 | Distributed data processing       |
| PySpark                      | Data transformation               |
| SQL / T-SQL                  | Data analysis                     |
| Git / GitHub                 | Version control and documentation |

---

## 📂 Dataset

The project uses **New York City Taxi trip data**.

The dataset contains information related to taxi trips and can be used to analyze:

* Trip distance
* Passenger count
* Pickup and drop-off information
* Payment information
* Fare amounts
* Total trip cost
* Trip duration
* Taxi zones

The original dataset is not stored in this GitHub repository because of its size.

---

## 🔄 Data Engineering Workflow

### Step 1 — Data Ingestion

Raw NYC Taxi data is stored in Azure Data Lake Storage Gen2.

```text
NYC Taxi Data
      ↓
Azure Data Lake Storage Gen2
```

### Step 2 — Data Exploration

Azure Synapse Serverless SQL is used to query and explore data directly from the data lake.

Key activities include:

* Schema inspection
* Row-level exploration
* Data profiling
* Null-value analysis
* Duplicate detection
* Basic aggregations

### Step 3 — Data Transformation

Data is transformed using SQL and/or Apache Spark.

Transformation activities include:

* Data type conversion
* Handling invalid records
* Filtering invalid trips
* Column selection
* Derived columns
* Aggregations

### Step 4 — Data Analysis

SQL queries are used to answer business questions related to:

* Average trip distance
* Passenger distribution
* Total fares
* Trip volume
* Payment methods
* Taxi usage patterns
* Revenue-related metrics

---

## 🧹 Data Quality Checks

The project includes validation checks such as:

* Null-value detection
* Invalid trip distances
* Invalid passenger counts
* Negative or invalid fare values
* Duplicate records
* Missing required fields

Example:

```sql
SELECT COUNT(*) AS invalid_trips
FROM taxi_data
WHERE trip_distance <= 0;
```

---

## 📊 Business Questions

The project investigates questions such as:

### 1. What is the average trip distance?

### 2. How does passenger count affect trip distance?

### 3. What are the most common payment methods?

### 4. Which taxi trips generate the highest revenue?

### 5. What is the distribution of trip distances?

### 6. How many trips contain invalid or missing values?

### 7. What are the most frequently used pickup and drop-off locations?

---

## 🗄️ SQL Analysis

Example analytical query:

```sql
SELECT
    passenger_count,
    COUNT(*) AS total_trips,
    AVG(trip_distance) AS avg_trip_distance,
    SUM(total_amount) AS total_revenue
FROM taxi_data
WHERE passenger_count > 0
  AND trip_distance > 0
GROUP BY passenger_count
ORDER BY passenger_count;
```

---

## 🔥 Spark / PySpark

Apache Spark can be used for distributed processing of the NYC Taxi dataset.

Example:

```python
df = spark.read.parquet("<ADLS_PATH>")

df_clean = (
    df
    .filter("trip_distance > 0")
    .filter("passenger_count > 0")
)

display(df_clean.limit(10))
```

---

## 📈 Key Insights

The project produces analytical insights related to:

* Taxi trip patterns
* Passenger behavior
* Trip distance
* Revenue
* Payment methods
* Data quality
* Geographic trip patterns

> Add your actual findings here after completing the analysis. Avoid adding estimated results.

---

## 📸 Screenshots

### Azure Synapse Workspace

![Synapse Workspace](screenshots/synapse-workspace.png)

### Serverless SQL Query

![Serverless SQL](screenshots/serverless-sql.png)

### Data Exploration

![Data Explorer](screenshots/data-explorer.png)

### Query Results

![Query Results](screenshots/query-results.png)

---

## 📁 Repository Structure

```text
├── architecture/
├── data/
├── synapse/
│   ├── serverless-sql/
│   ├── spark/
│   └── pipelines/
├── sql/
├── screenshots/
├── docs/
├── .gitignore
├── LICENSE
└── README.md
```

---

## 🚀 How to Reproduce the Project

### Prerequisites

You will need:

* Microsoft Azure subscription
* Azure Synapse Analytics workspace
* Azure Data Lake Storage Gen2
* Synapse Serverless SQL
* Apache Spark / PySpark if Spark processing is used
* Git / GitHub

### Setup

1. Create an Azure Data Lake Storage Gen2 account.
2. Upload the NYC Taxi dataset to the appropriate storage location.
3. Create or configure an Azure Synapse Analytics workspace.
4. Configure access between Synapse and the storage account.
5. Run the SQL scripts in `synapse/serverless-sql/`.
6. Run the Spark/PySpark notebooks or scripts if applicable.
7. Execute the analytical queries in `sql/`.
8. Review the generated results and insights.

---

## 🔐 Security

No Azure credentials, access keys, passwords, SAS tokens, connection strings, or other secrets are stored in this repository.

All sensitive configuration values must be kept outside source control.

---

## 📚 Key Data Engineering Concepts Demonstrated

* Cloud data storage
* Data lake architecture
* Azure Synapse Analytics
* Serverless SQL
* Apache Spark
* PySpark
* SQL analytics
* Data cleansing
* Data quality
* Data transformation
* Data exploration
* Analytical data processing
* Git and GitHub

---

## 🔮 Future Improvements

Potential future enhancements include:

* Azure Data Factory orchestration
* Incremental data processing
* Delta Lake
* Medallion architecture
* Automated data quality checks
* Power BI dashboard
* CI/CD
* Infrastructure as Code
* Monitoring and logging

---

## 👨‍💻 Author

**Shubham Prakash Jamdhade**

Aspiring Azure Data Engineer

**Core Skills:** Python | SQL | PySpark | Azure Data Factory | Azure Databricks | ADLS Gen2 | Delta Lake | Azure Synapse Analytics

---

⭐ If you find this project useful, consider giving the repository a star.
