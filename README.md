# End-to-End Customer Analytics Platform on AWS with Power BI

## 📌 Overview

- **Project Purpose:**  
  This project implements an end-to-end, cloud-native customer analytics platform to analyze customer churn and retention patterns using **AWS serverless analytics services** and **Power BI**.

- **What It Demonstrates:**  
  Raw customer data is ingested into a cloud data lake, automatically cataloged, queried using serverless SQL, and visualized through interactive dashboards — **without managing any infrastructure**.

- **Design Philosophy:**  
  The project is built as a **production-style analytics solution**, following industry best practices for:
  - Data lake architecture  
  - Metadata management  
  - Security and governance  
  - Business intelligence and reporting  

---

## 🎯 Problem Statement

- Customer churn is a critical business problem for subscription-based services.
- Organizations require a **scalable and cost-efficient analytics solution** to:
  - Understand **why customers churn**
  - Identify **high-risk customer segments**
  - Measure **revenue impact**
  - Enable **non-technical users** to explore insights

- **Solution:**  
  This project addresses these challenges by building a **fully serverless customer analytics platform on AWS**.

---

## 🏗️ Architecture

- **Data Ingestion:** Customer churn dataset uploaded to Amazon S3  
- **Metadata Management:** AWS Glue Crawlers infer schema and update Data Catalog  
- **Analytics Layer:** Amazon Athena executes SQL queries directly on S3  
- **Security & Governance:** IAM Roles and Athena Workgroups  
- **Visualization:** Power BI connects to Athena using ODBC  

---

## 🧩 Technology Stack & Role in This Project

### 🗄️ Amazon S3 – Data Lake
- **Role:** Centralized storage layer
- Stores customer churn dataset in two logical zones:
  - `/raw/` → Original source data
  - `/curated/` → Cleaned and analytics-ready data
- Provides durable, scalable, and low-cost storage
- Acts as the **single source of truth** for analytics

### 🤖 AWS Glue Crawler
- **Role:** Automated schema discovery
- Scans curated data stored in S3
- Infers column names and data types automatically
- Updates metadata without manual table creation
- Prevents schema drift issues

### 📚 AWS Glue Data Catalog
- **Role:** Central metadata repository
- Stores table definitions and schemas
- Enables Athena to understand S3 data structure
- Acts as the semantic layer between storage and analytics

### 🔎 Amazon Athena
- **Role:** Serverless analytics engine
- Executes SQL queries directly on S3 data
- No cluster or infrastructure management required
- Used to:
  - Perform churn analysis
  - Create analytical views
  - Prepare BI-ready datasets

### 🔐 IAM Roles & Athena Workgroups
- **Role:** Security and governance
- Enforces least-privilege access
- Controls access to S3, Glue, and Athena
- Athena workgroups manage:
  - Query execution
  - Cost tracking
  - Query result locations

### 📊 Power BI (via ODBC)
- **Role:** Visualization and reporting layer
- Connects to Athena using ODBC driver
- Imports analytical views
- Builds interactive dashboards
- Enables self-service analytics for business users

---

## ✨ Key Features

- Centralized cloud data lake using Amazon S3
- Automated schema inference using AWS Glue Crawlers
- Serverless SQL analytics with Amazon Athena
- Secure access control using IAM
- Interactive Power BI dashboards
- Cost-efficient and scalable architecture
- Easily extensible for advanced analytics

---

## 📂 Dataset

- **Source:** Kaggle – Telco Customer Churn
- **Format:** CSV

### Key Columns
- `customerID` – Unique customer identifier  
- `gender` – Customer gender  
- `seniorCitizen` – Senior citizen flag  
- `tenure` – Number of months with the service  
- `contract` – Contract type  
- `paymentMethod` – Payment method used  
- `monthlyCharges` – Monthly subscription cost  
- `totalCharges` – Lifetime customer charges  
- `churn` – Whether the customer churned (Yes/No)

---

## ⚙️ Step-by-Step Execution Guide

### ✅ Prerequisites
- AWS Account
- IAM role with access to:
  - Amazon S3
  - AWS Glue
  - Amazon Athena
- Power BI Desktop installed
- Amazon Athena ODBC Driver installed

---

### 🛠️ Step 1: Upload Dataset to Amazon S3
- Create an S3 bucket
- Create folders:
  - `/raw/`
  - `/curated/`
- Upload Telco churn CSV to:
  - `s3://<bucket-name>/raw/`
- Perform basic cleaning and store final dataset in:
  - `s3://<bucket-name>/curated/`

---

### 🛠️ Step 2: Configure AWS Glue Crawler
- Create a Glue crawler
- Set data source to:
  - `s3://<bucket-name>/curated/`
- Assign IAM role
- Run crawler
- Verify table creation in Glue Data Catalog

---

### 🛠️ Step 3: Validate Glue Data Catalog
- Confirm database and table names
- Verify inferred schema
- Ensure correct data types

---

### 🛠️ Step 4: Configure Amazon Athena
- Create an Athena workgroup
- Set query result location in S3
- Run SQL queries to:
  - Explore data
  - Create analytical views
  - Compute churn KPIs
- SQL scripts are included in the repository

---

### 🛠️ Step 5: Install and Configure Athena ODBC
- Install Athena ODBC driver
- Configure DSN with:
  - AWS region
  - Athena workgroup name
  - S3 output location

---

### 🛠️ Step 6: Connect Power BI
- Open Power BI Desktop
- Connect via ODBC
- Import Athena views
- Build dashboards and reports

---

## 📊 Power BI Dashboards

- Overall churn rate
- Churn by contract type
- Churn by services
- Tenure-based segmentation
- Revenue impact of churn
- High-risk customer identification

---

## 🔮 Future Enhancements

- Integrate AWS SageMaker for churn prediction
- Automate ingestion using AWS Lambda
- Add data partitioning for performance optimization
- CI/CD pipelines for analytics workflows
