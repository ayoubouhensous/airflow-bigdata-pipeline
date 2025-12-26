# Big Data Pipeline with Apache Airflow

This project implements a **complete Big Data pipeline orchestrated with Apache Airflow**, using a **lakehouse-style architecture**.  
The pipeline handles data ingestion, validation, transformation, and loading into a curated layer ready for **analytics and machine learning**.

---

## 🧩 Pipeline Overview

The DAG `bigdata_pipeline_complete` executes the following tasks:

1️⃣ **Data Ingestion**
- Generates a raw dataset (`sales.csv`)
- Stores raw data in the `raw` layer  
📂 `./data/raw`

2️⃣ **Data Validation**
- Checks if the raw dataset exists
- Prevents pipeline execution if data is missing

3️⃣ **Data Transformation**
- Cleans and processes raw data
- Outputs processed data to the `processed` layer  
📂 `./data/processed`

4️⃣ **Load to Lakehouse**
- Moves processed data to the curated layer
- Prepares data for analytics and ML workloads  
📂 `./data/curated`

5️⃣ **Analytics / ML Ready**
- Confirms that data is ready for BI / ML

### 🔗 Pipeline Workflow

```

Ingest → Validate → Transform → Load (Lakehouse) → Analytics

````

- **Schedule:** Daily
- **Executor:** LocalExecutor
- **Database:** PostgreSQL

---

## 🐳 Docker Compose Architecture

The project uses **Docker Compose** to deploy and manage Airflow services:

### 📦 Services Included

- **PostgreSQL**
  - Stores Airflow metadata
- **Airflow Webserver**
  - Provides Airflow Web UI
- **Airflow Scheduler**
  - Executes DAG tasks

### ⚙️ Volumes Mounted

- `./dags` → Airflow DAGs
- `./data` → Raw, processed, and curated data

---

## 🏁 How to Run the Pipeline (First Time Setup)

### 1️⃣ Initialize the Airflow metadata database *(run once)*

```bash
docker-compose run airflow-webserver airflow db init
````

---

### 2️⃣ Create the Airflow admin user *(run once)*

```bash
docker-compose run airflow-webserver airflow users create \
  --username airflow \
  --password airflow \
  --firstname Airflow \
  --lastname Admin \
  --role Admin \
  --email admin@airflow.local
```

---

### 3️⃣ Start Airflow services

```bash
docker-compose up -d
```

---

### 4️⃣ Access the Airflow Web UI

Open your browser:

```
http://localhost:8080
```

**Login credentials:**

* **Username:** airflow
* **Password:** airflow

---

### 5️⃣ Trigger the Pipeline DAG

* In the Airflow Web UI, go to **DAGs**
* Locate `bigdata_pipeline_complete`
* **Turn on** the DAG
* Either **wait for the daily schedule** or **trigger manually**

---

### 6️⃣ Verify Data Layers

After the DAG runs successfully:

* **Raw layer:** `./data/raw/sales.csv`
* **Processed layer:** `./data/processed/sales_clean.csv`
* **Curated layer:** `./data/curated/sales_curated.csv`

---

### 7️⃣ Ready for Analytics / ML

* Data is clean and ready for **Business Intelligence** or **Machine Learning tasks**.
* Connect your BI tools or ML scripts directly to the curated layer.

---

## 📂 Project Structure

```
.
├── dags/
│   └── bigdata_pipeline_complete.py
├── data/
│   ├── raw/
│   ├── processed/
│   └── curated/
├── docker-compose.yml
└── README.md
```
## 🖥️ Airflow Interfaces

This project provides the standard **Airflow Web UI** interfaces to monitor and manage your pipeline.

### 1️⃣ Login Page

* Use this page to log into Airflow with the admin user you created.
* Default credentials:

```
Username: airflow
Password: airflow
```

![Airflow Login](https://raw.githubusercontent.com/ton-repo/screenshots/login.png)

---

### 2️⃣ Dashboard (DAGs View)

* Shows all available DAGs, including `bigdata_pipeline_complete`.
* Allows you to **activate, pause, and trigger DAGs**.

![Airflow Dashboard](https://raw.githubusercontent.com/ton-repo/screenshots/dashboard.png)

---

### 3️⃣ Graph View (Execution Flow)

* Visual representation of the DAG workflow.
* Shows **task dependencies** and **execution status**.
* Helps monitor the ETL pipeline step by step.

![Airflow Graph View](https://raw.githubusercontent.com/ton-repo/screenshots/graph.png)

---

---

## ✅ Key Features

* End-to-end ETL pipeline
* Airflow orchestration
* Lakehouse-style data layers
* Dockerized deployment
* Ready for BI & Machine Learning

```
