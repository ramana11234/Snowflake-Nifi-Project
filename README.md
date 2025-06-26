# 🚀 Snowflake-NiFi-Project

This project showcases a fully automated, real-time data pipeline integrating **Apache NiFi**, **Snowflake**, and **AWS EC2**, all orchestrated using **Docker** containers. It demonstrates how raw data can be generated, moved, stored, and processed in a completely automated and scalable manner.

---

## 🧩 Project Architecture Overview

1. **Data Generation**:
   - Data is created using a **Jupyter Notebook** running on a **Dockerized EC2 instance**.
   - The generated data is saved locally in a `.csv` format.

2. **Data Orchestration with Apache NiFi**:
   - **Apache NiFi**, also running in Docker, is used to automatically fetch the newly created CSV file.
   - NiFi flows are designed to:
     - Monitor the local directory.
     - Read the new data.
     - Push the data into a specified **Amazon S3 bucket**.

3. **Cloud Storage (Amazon S3)**:
   - Acts as an intermediary storage layer.
   - NiFi uploads the data to a pre-configured S3 bucket securely and automatically.

4. **Snowflake Integration**:
   - A **Snowflake stage** is created to reference the S3 bucket.
   - **Snowflake external tables** are used to read data from S3.
   - **Streams and Tasks** in Snowflake detect changes in external data and update internal tables.

5. **Data Flow Management**:
   - One table maintains the raw, unaltered data.
   - Another table keeps track of real-time updates (handled via Snowflake’s change tracking and transformation logic).

---

## 🔧 Tools & Technologies Used

- **Amazon EC2** – Cloud server to host the entire pipeline
- **Docker** – Containerization of all services
- **Apache NiFi** – Data flow and integration tool
- **Jupyter Notebook** – For data generation
- **Apache ZooKeeper** – Service coordination (optional but configured)
- **Amazon S3** – Cloud storage for intermediate data
- **Snowflake** – Cloud data warehouse for processing and storage
  - **Stages**
  - **External Tables**
  - **Streams**
  - **Tasks**

---

## 📁 Project Structure

Snowflake-Nifi-Project/
├── docker-compose.yml             # Docker config for NiFi, Jupyter, ZooKeeper
├── notebooks/
│   └── data_generator.ipynb       # Jupyter Notebook to generate sample data
├── nifi_flows/
│   └── nifi_flow.xml              # Apache NiFi flow definition (exported template)
├── snowflake/
│   ├── create_stage.sql           # Script to create external stage and table
│   └── streams_and_tasks.sql      # Script for Snowflake streams and tasks
├── s3_bucket/                     # (Optional) Local folder to mimic S3 bucket during testing
│   └── sample_data.csv
└── README.md                      # Project documentation
