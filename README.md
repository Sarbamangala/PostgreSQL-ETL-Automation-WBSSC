# HR Recruitment Data Migration & Automation (WBSSC)

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


