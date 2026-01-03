#End-to-End Customer Analytics Platform on AWS with Power BI
📌 Overview

This project implements an end-to-end, cloud-native customer analytics platform to analyze customer churn and retention patterns using AWS serverless analytics services and Power BI.

The platform demonstrates how raw customer data can be ingested into a cloud data lake, automatically cataloged, queried using serverless SQL, and visualized through interactive dashboards — without managing any infrastructure.

This project is designed as a production-style analytics solution, following industry best practices for data lake architecture, metadata management, security, and business intelligence.

🎯 Problem Statement

Customer churn is a critical business problem for subscription-based services.
Organizations need a scalable and cost-efficient way to:

Understand why customers churn

Identify high-risk customer segments

Measure revenue impact

Enable business users to explore insights without technical complexity

This project addresses these needs by building a fully serverless analytics platform on AWS.

🏗️ Architecture



🧩 Technology Stack & Role in This Project
🗄️ Amazon S3 – Data Lake

Role: Centralized storage layer

Stores customer churn dataset in two logical zones:

/raw/ → original source data

/curated/ → cleaned and analytics-ready data

Provides durable, scalable, low-cost storage

Acts as the single source of truth for analytics

🤖 AWS Glue Crawler

Role: Automated schema discovery

Scans curated data stored in S3

Infers column names and data types automatically

Updates metadata without manual table creation

Eliminates schema drift issues

📚 AWS Glue Data Catalog

Role: Central metadata repository

Stores table definitions and schemas

Enables Athena to understand S3 data structure

Acts as the semantic layer between storage and analytics

🔎 Amazon Athena

Role: Serverless analytics engine

Executes SQL queries directly on S3 data

No cluster or infrastructure management

Used to:

Perform churn analysis

Create analytical views

Prepare BI-ready datasets

🔐 IAM Roles & Athena Workgroups

Role: Security and governance

Enforces least-privilege access

Controls access to S3, Glue, and Athena

Athena workgroups manage:

Query execution

Cost tracking

Query result locations

📊 Power BI (via ODBC)

Role: Visualization & reporting layer

Connects to Athena using ODBC driver

Imports analytical views

Builds interactive dashboards for business users

Enables self-service analytics

✨ Key Features

Centralized cloud data lake using Amazon S3

Automated schema inference using AWS Glue Crawlers

Serverless SQL analytics with Amazon Athena

Secure access control using IAM

Interactive Power BI dashboards

Cost-efficient and scalable architecture

Easily extensible for predictive analytics

📂 Dataset

Source: Kaggle – Telco Customer Churn

Format: CSV
Key Columns

customerID – Unique customer identifier

gender – Customer gender

seniorCitizen – Senior citizen flag

tenure – Number of months with the service

contract – Contract type

paymentMethod – Payment method used

monthlyCharges – Monthly subscription cost

totalCharges – Lifetime customer charges

churn – Whether the customer churned (Yes/No)

⚙️ Step-by-Step Execution Guide

This section explains exactly how someone else can reproduce the project.

✅ Prerequisites

AWS Account

IAM role with access to:

Amazon S3

AWS Glue

Amazon Athena

Power BI Desktop installed

Amazon Athena ODBC Driver installed

🛠️ Step 1: Upload Dataset to Amazon S3

Create an S3 bucket

Create folders:

/raw/
/curated/


Upload the Telco churn CSV to:

s3://<bucket-name>/raw/


Perform basic cleaning and store final dataset in:

s3://<bucket-name>/curated/

🛠️ Step 2: Configure AWS Glue Crawler

Create a Glue crawler

Set data source to:

s3://<bucket-name>/curated/


Assign IAM role

Run crawler

Verify table creation in Glue Data Catalog

🛠️ Step 3: Validate Glue Data Catalog

Confirm database and table names

Verify inferred schema

Ensure data types are correct

🛠️ Step 4: Configure Amazon Athena

Create an Athena workgroup

Set query result location in S3

Run SQL queries to:

Explore data

Create analytical views

Compute churn KPIs

(SQL files are available in the repository.)

🛠️ Step 5: Install and Configure Athena ODBC

Install Athena ODBC driver

Configure DSN with:

AWS region

Workgroup name

S3 output location

🛠️ Step 6: Connect Power BI

Open Power BI Desktop

Connect via ODBC

Import Athena views

Build dashboards and reports

📊 Power BI Dashboards

The dashboards provide insights such as:

Overall churn rate

Churn by contract type

Churn by services

Tenure-based segmentation

Revenue impact of churn

High-risk customer identification

📁 Repository Structure
├── README.md
├── architecture/
│   └── end_to_end_customer_analytics_architecture.png
├── analytics_sql_layer/
│   └── customer_churn_analysis.sql
├── customer_data_assets/
│   └── telco_customer_churn.csv
├── powerbi_analytics_layer/
│   ├── customer_churn_retention_dashboard.pbix
│   └── powerbi_visual_exports/
├── pipeline_execution_evidence/

🔮 Future Enhancements

Integrate AWS SageMaker for churn prediction

Automate ingestion using AWS Lambda

Add partitioning for performance optimization

CI/CD for analytics workflows

🏁 Conclusion

This project demonstrates how to build a scalable, serverless customer analytics platform on AWS that delivers real business insights through Power BI.
It reflects real-world data engineering practices and can be extended to production-grade analytics systems.
