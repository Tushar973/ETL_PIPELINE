# Airflow ETL Pipeline with Postgres and API Integration

## 📌 Project Overview

This project implements an **ETL (Extract, Transform, Load) pipeline** using **Apache Airflow**. The pipeline extracts data from an external API—**NASA’s Astronomy Picture of the Day (APOD) API**—transforms the data, and loads it into a **PostgreSQL database**.

The entire workflow is orchestrated using **Apache Airflow**, which enables scheduling, monitoring, and managing data pipelines efficiently. The project uses **Docker** to run both Airflow and Postgres in isolated, reproducible containers.

---

## 🛠️ Key Technologies Used

- **Apache Airflow** – Workflow orchestration
- **PostgreSQL** – Data storage
- **Docker & Docker Compose** – Containerized environment
- **NASA APOD API** – External data source
- **Python** – ETL logic

---

## 🧩 Key Components

### 1. Airflow for Orchestration
- Defines and manages the ETL workflow using a **DAG (Directed Acyclic Graph)**.
- Handles task dependencies and scheduling.
- Uses both **classic operators** and **TaskFlow API**.
- Ensures reliable and sequential execution of tasks.

### 2. PostgreSQL Database
- Stores extracted and transformed data.
- Runs inside a Docker container.
- Data persistence is handled using Docker volumes.
- Interactions are managed via:
  - `PostgresHook`
  - `PostgresOperator`

### 3. NASA APOD API
- Provides daily astronomy-related data.
- Returns data in JSON format, including:
  - Title
  - Explanation
  - Image URL
  - Date
- Data is extracted using Airflow’s `SimpleHttpOperator`.

---

## 🎯 Project Objectives

### Extract Data
- Fetch daily astronomy data from NASA’s APOD API.

### Transform Data
- Process the raw JSON response.
- Extract relevant fields.
- Ensure data is properly formatted for database insertion.

### Load Data
- Insert transformed data into a PostgreSQL table.
- Automatically create the table if it does not exist.

---

## 🏗️ Architecture & Workflow

The ETL pipeline is orchestrated through an **Airflow DAG**, consisting of the following stages:

### 1. Extract (E)
- Uses `SimpleHttpOperator` to send an HTTP GET request to the NASA APOD API.
- Retrieves data in JSON format.
- Captures key fields such as:
  - `title`
  - `explanation`
  - `url`
  - `date`

### 2. Transform (T)
- Implemented using Airflow’s **TaskFlow API** with the `@task` decorator.
- Parses the JSON response.
- Selects and formats the required fields.
- Prepares data for database insertion.

### 3. Load (L)
- Uses `PostgresHook` to insert data into PostgreSQL.
- Includes a task to create the target table if it does not already exist.
- Ensures idempotent and reliable data loading.

---

## 🚀 Outcome

- A fully automated daily ETL pipeline.
- Clean and structured data stored in PostgreSQL.
- Scalable and reproducible workflow using Docker and Airflow.
- Ready for downstream analytics, reporting, or visualization.

---

## 📅 Scheduling

- The DAG is scheduled to run **daily**, automatically fetching and storing the latest APOD data.

---

## ✅ Future Enhancements (Optional)

- Add data validation checks.
- Implement logging and alerting.
- Extend to support additional NASA APIs.
- Visualize data using BI tools.

---

⭐ If you find this project useful, feel free to star the repository!
