## Project 1: HR Recruitment Data Migration & Automation (WBSSC)

[cite_start]This repository contains the complete production-ready SQL architecture, ETL pipeline documentation, and optimization strategies utilized to migrate and automate historical legacy recruitment logs at the West Bengal Staff Selection Commission (WBSSC)[cite: 26, 56].

## 1. Project Architecture Overview

| Phase | Source System / Tool | Action / SQL Command | Output / Business Value |
| :--- | :--- | :--- | :--- |
| **Data Extraction** | MS Access | Export raw recruitment application logs & assessment marks | [cite_start]Centralized unstructured candidate ingestion pool  |
| **Data Migration** | PostgreSQL (pgAdmin / psql) | `CREATE TABLE` & schema mapping for candidate database | [cite_start]High-performance relational storage with optimized indexing  |
| **Data Processing** | PostgreSQL Engine | `ORDER BY assessment_marks DESC` (Sorting & Ranking) | [cite_start]Identifies top talent transparently across metrics  |
| **Business Logic** | PostgreSQL Query / `WHERE` | Filtering based on dynamic Cutoff Marks (e.g., $\ge 75$) | [cite_start]Automated shortlisting, eliminating manual resume screening [cite: 40, 57] |
| **Data Exportation** | PostgreSQL `COPY TO` Command | `COPY (SELECT...) TO 'path/shortlist.csv' WITH CSV HEADER` | [cite_start]Generates clean, production-ready CSV files for Stakeholders  |

---

## 2. Production-Ready SQL Script & Workflow

### Step 1: Table Schema Creation
```sql
CREATE TABLE recruitment_data (
    candidate_id SERIAL PRIMARY KEY,
    candidate_name VARCHAR(100),
    email VARCHAR(100),
    assessment_marks NUMERIC(5,2),
    applied_role VARCHAR(50)
);
\copy recruitment_data FROM '/path/to/access_raw_data.csv' DELIMITER ',' CSV HEADER;
SELECT candidate_id, candidate_name, assessment_marks
FROM recruitment_data
WHERE assessment_marks >= 75.00
ORDER BY assessment_marks DESC;


COPY (
     SELECT candidate_id, candidate_name, assessment_marks
     FROM recruitment_data
     WHERE assessment_marks >= 75.00
     ORDER BY assessment_marks DESC
) TO '/var/lib/postgresql/data/shortlisted_candidates.csv' WITH CSV HEADER;

## Project 2: Robotic Automation Workflow Optimization & Predictive Analytics (Kawasaki Robotics)

# Robotic Automation Workflow Optimization & Predictive Analytics

This repository contains the predictive modeling framework, workflow automation logic, and telemetry data processing pipelines designed to optimize robotic asset utilization and forecast machine performance anomalies.

## 1. Project Architecture Overview

| Phase | Core Technology / Library | Action / Method Implemented | Output / Business Value |
| :--- | :--- | :--- | :--- |
| **Data Ingestion** | Python, Real-time Logging | Ingestion of high-frequency robotic telemetry and log streams | Ensured data pipeline integrity for high-accuracy raw data processing |
| **Data Cleaning** | Pandas, NumPy | Outlier removal, time-alignment, and noise filtering of sensor data | Cleaned dataset ready for statistical analysis and feature engineering |
| **Predictive Modeling**| SciPy (Statistical Models) | Implemented advanced regression and Predictive Value Measurement | Forecasted machine performance and minimized deployment anomalies |
| **Business Logic** | Python, Math Frameworks | Translated complex predictive datasets into operational metrics | Optimized robotic automation workflows and improved asset utilization |

---

## 2. Production-Ready Python Framework & Workflow

### Step 1: Telemetry Data Processing & Anomaly Detection
```python
import numpy as np
import pandas as pd
from scipy import stats

# Simulating high-frequency robotic telemetry data (Timestamp, Temperature, Vibration, Status)
data = {
    'timestamp': pd.date_range(start='2026-01-01', periods=1000, freq='s'),
    'vibration_level': np.random.normal(loc=50, scale=5, size=1000),
    'temperature_celsius': np.random.normal(loc=75, scale=8, size=1000)
}
df = pd.DataFrame(data)

# Z-score calculation to detect deployment anomalies in vibration levels
df['vibration_z_score'] = np.abs(stats.zscore(df['vibration_level']))
anomalies = df[df['vibration_z_score'] > 3]

print(f"Total Telemetry Anomalies Detected: {len(anomalies)}")
from scipy.stats import linregress

# Linear regression to forecast temperature drift over time to prevent machine failure
slope, intercept, r_value, p_value, std_err = linregress(df.index, df['temperature_celsius'])

print(f"Predictive Trend Slope: {slope:.5f} (Temperature change per second)")
print(f"Model Confidence (R-squared): {r_value**2:.4f}")


## Project 3: E-Commerce User Behavior Analytics & Reporting Pipeline (Flipkart Case Study)
# E-Commerce User Behavior Analytics & Reporting Pipeline

An end-to-end data processing and business intelligence project focused on constructing scalable SQL analytics, executing user drop-off trend analysis, and deploying automated reporting workflows.

## 1. Project Architecture Overview

| Phase | Source System / Tool | Action / Implementation Strategy | Output / Business Value |
| :--- | :--- | :--- | :--- |
| **Data Transformation**| Python (Pandas, NumPy) | Built transformation pipelines for raw application transactional files | Reduced data ingestion errors and standardized unstructured metrics |
| **Advanced SQL** | PostgreSQL (CTEs, Window) | Engineered scalable queries with tracking (`RANK`, `LAG`, `LEAD`) | Identified user drop-off trends across conversion funnels |
| **Data Modeling** | Relational Database | Partnered with business teams to structure raw transactional data | Designed optimized dimensional models for production analytics |
| **BI Reporting** | Power BI | Deployed automated executive interactive dashboards | Optimized cross-functional reporting efficiency by 30% |

---

## 2. Production-Ready Analytics Scripts

### Step 1: SQL Conversion Funnel & Drop-Off Analysis
```sql
-- Using CTEs and Window Functions to analyze user journey sessions and identify drop-off points
WITH UserSessionFunnels AS (
    SELECT 
        user_id,
        session_id,
        page_type,
        action_timestamp,
        LEAD(page_type) OVER (PARTITION BY user_id ORDER BY action_timestamp) AS next_page
    FROM ecommerce_logs
)
SELECT 
    page_type AS current_stage,
    next_page AS drop_off_stage,
    COUNT(user_id) AS total_users_dropped
FROM UserSessionFunnels
WHERE next_page IS NULL OR next_page = 'cart_abandoned'
GROUP BY page_type, next_page
ORDER BY total_users_dropped DESC;
import pandas as pd

# Automated data cleaning pipeline for raw e-commerce ingestion
def clean_ecommerce_data(file_path):
    df = pd.read_csv(file_path)
    
    # Fill missing values and eliminate ingestion errors
    df['user_id'] = df['user_id'].fillna(-1).astype(int)
    df['transaction_amount'] = df['transaction_amount'].fillna(0.0)
    
    # Filtering out system anomalies
    cleaned_df = df[df['transaction_amount'] >= 0]
    return cleaned_df

print("ETL Pipeline initialized successfully.")
