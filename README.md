
# Retention-Focused User Engagement Pipeline

This project simulates real-world website user activity, builds a robust data pipeline using **Python**, **Airflow**, and **PostgreSQL**, applies dimensional modeling with **SCD Type 2** support, performs data quality checks using **Great Expectations**, and visualizes both **business KPIs** (via Looker Studio) and **operational metrics** (via Grafana). The goal is to showcase strong data engineering practices suitable for modern analytics and growth-focused teams.

## 🧠 Project Purpose

To demonstrate a complete, production-grade data engineering pipeline that:
- Handles **messy, real-world user activity data**
- Tracks **user retention**, **engagement patterns**, and **sales performance**
- Applies dimensional modeling (fact/dim tables + SCD Type 2)
- Implements automated **data quality validation**
- Provides both **business** and **engineering observability**

## ⚙️ Architecture Overview

[Python Faker] → [Airflow DAG] → [PostgreSQL] → [Great Expectations]
                                 ↓
                   [Grafana]   [Looker Studio]

- **Data Generation**: Synthetic clickstream and purchase data over a full calendar year
- **Orchestration**: Airflow automates data ingestion, validation, and transformation
- **Storage**: PostgreSQL stores raw and transformed data in dimensional models
- **Validation**: Great Expectations enforces data quality gates
- **Visualization**: Grafana tracks pipeline metrics; Looker Studio shows KPIs

## 🧱 Stack

| Component        | Tool                  |
|------------------|-----------------------|
| Language         | Python 3.10+          |
| Storage          | PostgreSQL (local)    |
| Orchestration    | Apache Airflow        |
| Validation       | Great Expectations    |
| Visualization    | Looker Studio, Grafana |
| Data Generation  | Faker, Pandas         |

## 📁 Project Structure

.
├── dags/                      # Airflow DAGs for orchestration
├── data_generator/            # Python scripts using Faker
├── sql/                       # DDLs for fact/dim tables, transformations
├── validation/                # Great Expectations config
├── dashboards/                # Looker and Grafana setup info
├── README.md
├── requirements.txt
└── .env (excluded)

## 🗃️ Data Model

### ⭐ Fact Table
- `fact_user_events`: All user events (clicks, page views, purchases)

### 🧊 Dimension Tables
- `dim_user`: SCD Type 2 tracked user attributes (location, device, etc.)
- `dim_product`: Product metadata
- `dim_date`: Calendar dimension

### 📦 Compressed Engagement Modeling
- `fact_user_weekly_summary`: Stores arrays like `[3,2,0,4,1,1,2]` representing daily engagement to reduce row count

## 📊 Metrics Tracked

### 📈 Business Analytics (Looker Studio)
- Weekly/Monthly Sales
- Retention & Engagement
- Funnel Conversion: Page View → Cart → Purchase
- Product Popularity

### 🛠️ Operational Metrics (Grafana)
- DAG run duration
- Data load volume
- Validation pass/fail counts
- Row count deltas

## 🔒 Data Quality Checks

Using **Great Expectations** to validate:
- Null checks on key columns (`user_id`, `event_type`)
- Timestamp sanity (future/past range)
- Primary key uniqueness
- Categorical field validity (`event_type` in allowed list)

## 🕒 Ingestion and Simulation Details

- Simulates a full **365-day** period (to enable retention and cohort analysis)
- Only **7 days of data generated** in real-time; timestamps span the year
- Total size is kept under **100 MB**
- One Airflow DAG run = one synthetic day ingested

## 🚀 Setup & Usage

### 1. Install Requirements

pip install -r requirements.txt

### 2. Set Up PostgreSQL

Create a database and tables using the scripts in `/sql/ddl/`.

### 3. Initialize Airflow

export AIRFLOW_HOME=~/airflow
airflow db init
airflow webserver -p 8080
airflow scheduler

### 4. Run DAG

Use the Airflow UI or CLI to trigger the daily simulation DAG.

## 📌 Status

✅ MVP complete  
🔄 Additional enhancements in progress:
- Add CI/CD support  
- Simulate seasonal behavior patterns  
- Include alerting on validation failures

## 📄 License

MIT License

## ✍️ Author

Naman Gala — Data Engineer | LinkedIn
