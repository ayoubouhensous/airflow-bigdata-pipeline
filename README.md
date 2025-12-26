
## 🚀 Running Apache Airflow (First Time Setup)

When using **Apache Airflow for the first time**, the metadata database **must be initialized**.
Without this step, Airflow services will not start correctly.

### 1️⃣ Initialize the Airflow metadata database *(run once)*

```bash
docker-compose run airflow-webserver airflow db init
```

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

Open your browser and go to:

```
http://localhost:8080
```

---

### 🔐 Default Login Credentials

* **Username:** `airflow`
* **Password:** `airflow`
