# Azure Synapse E-commerce Data Engineering Architecture

## Overview
This project implements an end-to-end data engineering pipeline using Azure Synapse Analytics and Azure Data Lake Storage Gen2.

The goal is to process raw e-commerce data and build an analytics layer for reporting and business insights.

The architecture follows the **Medallion Architecture** pattern.

Raw → Silver → Gold

---

## Architecture Diagram
E-commerce Dataset (CSV)
↓
Azure Data Lake Storage Gen2 (Raw Layer)
↓
Synapse Spark Notebook (Silver Transform)
↓
Parquet Data Storage (Silver Layer)
↓
Synapse Spark Transformations (Gold Layer)
↓
Synapse Serverless SQL Views
↓
Power BI Dashboard


---

## Technology Stack

| Component | Technology |
|--------|-------------|
| Storage | Azure Data Lake Storage Gen2 |
| Processing | Synapse Spark (PySpark) |
| Orchestration | Synapse Pipelines |
| Query Engine | Synapse Serverless SQL |
| Visualization | Power BI |
| Data Format | Parquet |

---

## Data Flow

### 1. Data Ingestion (Raw Layer)

The Olist e-commerce dataset is uploaded to Azure Data Lake Storage.

Raw data is stored without modification.

Example structure:

raw/

customers/
orders/
order_items/
products/
order_payments/

---

### 2. Silver Layer Transformation

Synapse Spark notebooks clean and transform the raw data.

Transformations include:

- Removing duplicate records
- Casting data types
- Handling null values
- Converting timestamps
- Standardizing schemas

The processed data is stored in **Parquet format** for improved query performance.

silver/

customers/
orders/
order_items/
products/
order_payments/

---

### 3. Gold Layer Modeling

The Gold layer contains business-ready data optimized for analytics.

A **Star Schema** is created with fact and dimension tables.

Fact Tables:

fact_sales

Dimension Tables:

dim_customer
dim_product

This layer supports reporting and analytical queries.

gold/

fact_sales/
dim_customer/
dim_product/

---

### 4. SQL Analytics Layer

Synapse Serverless SQL Pool queries Parquet files directly from the Gold layer using OPENROWSET.

SQL views are created to simplify analytics queries.

Example:

vw_fact_sales
vw_dim_customer
vw_dim_product

---

### 5. Data Visualization

Power BI connects to the Synapse Serverless SQL endpoint.

Dashboards provide insights including:

- Monthly revenue trends
- Top selling products
- Revenue by region
- Customer purchase behavior

---

## Medallion Architecture

This project follows a Medallion Architecture.

Raw Layer  
Stores original ingested data.

Silver Layer  
Contains cleaned and transformed datasets.

Gold Layer  
Contains analytics-ready fact and dimension tables.

---

## Key Benefits of the Architecture

- Scalable storage using Azure Data Lake
- Distributed data processing using Spark
- Cost-effective analytics using Serverless SQL
- Efficient query performance using Parquet format
- Integration with Power BI for business reporting

---

## Future Improvements

Potential enhancements to this architecture include:

- Incremental data pipelines
- Data quality validation
- Partitioning for large datasets
- CI/CD deployment pipelines
- Streaming ingestion

