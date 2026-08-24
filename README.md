# E-Commerce Data Engineering Project
## Azure Databricks – Bronze, Silver and Gold Data Pipeline

---

## 1. Project Overview

This project implements an end-to-end data engineering pipeline using Azure Databricks.

The source data consists of e-commerce CSV files stored in Azure Data Lake Storage Gen2 (ADLS Gen2). The data is processed through the Bronze, Silver and Gold layers to create trusted and business-ready datasets for reporting and analytics.

The pipeline uses Azure Databricks, Unity Catalog, PySpark, Parquet, Delta Lake and Databricks Workflows.

---

## 2. Business Requirement

The e-commerce company receives daily CSV files containing:

- Customer master data
- Product master data
- Order transaction data

The objective is to:

1. Read source CSV files from ADLS Gen2.
2. Preserve the source data in the Bronze layer.
3. Store Bronze data in Parquet format.
4. Add ingestion metadata.
5. Clean and validate the data in the Silver layer.
6. Maintain current customer, product and order records using SCD Type 1 MERGE.
7. Create business-ready sales data in the Gold layer.
8. Create summary datasets for reporting.
9. Automate the complete pipeline using a Databricks Workflow.
10. Validate the pipeline with new incoming order data.

---

# 3. Source Data

The source files are stored in Azure Data Lake Storage Gen2.

### customers.csv

Columns:

- customer_id
- customer_name
- city
- state

Purpose:

Customer master data.

### products.csv

Columns:

- product_id
- product_name
- category
- price

Purpose:

Product master data.

### orders.csv

Columns:

- order_id
- customer_id
- product_id
- order_date
- quantity

Purpose:

Daily order transaction data.

---

# 4. ADLS Gen2 Authentication

Azure Databricks accesses the ADLS Gen2 source location using an Azure Databricks Access Connector with Managed Identity authentication.

The managed identity was granted the required permissions to access the ADLS Gen2 storage location.

A Unity Catalog External Location was configured to provide controlled access to the source data.

No storage account access keys or secrets are stored directly in the Databricks notebooks.

### Authentication Flow

```text
Azure Databricks
       |
       | Managed Identity
       v
Azure Databricks Access Connector
       |
       v
Unity Catalog External Location
       |
       v
ADLS Gen2
       |
       | CSV Files
       v
Bronze Layer
