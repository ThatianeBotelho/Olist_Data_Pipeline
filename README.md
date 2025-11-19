# Olist E-commerce Analytics – End-to-End Data Pipeline
This project implements a complete data pipeline for the Olist Brazilian e-commerce dataset, using a modern Lakehouse architecture (Bronze → Silver → Gold).
The solution transforms raw multi-source transactional data into a curated analytics-ready model designed for business analysis and BI consumption.

# Dataset Overview
The Olist dataset represents a real e-commerce marketplace with multiple interconnected entities:
- Orders
- Order Items
- Customers
- Sellers
- Products
- Payments
- Reviews
This diversity enables realistic scenarios for data engineering, enrichment, dimensional modeling, and analytical insights.

# Business Context
Olist connects sellers from all over Brazil to customers purchasing through the marketplace.
This project answers key business questions such as:
- How does revenue evolve by region, category, seller, and time?
- Which customers and sellers drive the greatest value?
- What is the impact of freight and delivery delays?
- How do payment methods influence total order value?
- How is customer satisfaction reflected through review scores?

# Architecture (Lakehouse)
The pipeline follows a medallion-style architecture:
- Bronze – Raw ingestion of CSV files into Delta tables with minimal processing.
- Silver – Cleaned, standardized, conformed, and enriched data.
- Gold – Curated analytics model using a Star Schema (dimensions + fact table).

# Gold Layer – Star Schema
Fact Table:
- fact_sales
  - order_id, order_item_id
  - customer_key, seller_key, product_key
  - order_purchase_date_key, order_approved_date_key, delivery_date_key
  - metrics: price, freight_value, total_value, revenue
  - indicators: is_delayed, delivery_delay_days
  - optional: review_score, estimated_margin

Dimension Tables:
- dim_customer
  - location (city, state, region)
  - first/last purchase dates
  - total_revenue, order_count, avg_ticket
  - dim_seller
  - seller location
  - performance metrics

- dim_product
  - category, weight, size, volume
  - avg_price, items_sold
    
- dim_date
  - full calendar structure (year, month, day, week, quarter, flags)

# Tech Stack
- Databricks Community Edition – PySpark, Delta Lake, Databricks Jobs
- Python
- Power BI Desktop – BI layer consuming Gold tables

# Pipeline Components
- Bronze
  - Raw ingestion from Olist CSVs
  - Type normalization
  - Addition of ingestion metadata
  - Storage as Delta tables
- Silver
  - Data cleaning (nulls, formats, deduplication)
  - Conformance and normalization
  - Enrichment (revenue metrics, delay indicators, aggregated payments)
  - Multi-table integration into silver_sales
- Gold
  - Dimensional modeling using surrogate keys
  - Creation of fact and dimension tables
  - Business logic metrics ready for BI consumption

# Orchestration
A Databricks Job can orchestrate the pipeline execution in the following order:
- Bronze ingestion
- Silver transformations
- Gold model creation

# BI Layer
A Power BI report connected to the Gold layer provides:
- Revenue trends
- Seller and product performance
- Delivery and logistics KPIs
- Customer segmentation
- Review-based satisfaction indicators

# Repository Structure
olist-data-pipeline/
  README.md
  data_raw/
  notebooks/
  src/
    config.py
    utils/
  orchestration/
  docs/

# How to Run
1. Download the Olist dataset from Kaggle and place the CSV files under data_raw/.
2. Import the notebooks into Databricks Community Edition.
3. Configure paths in config.py.
4. Execute in order:
- 01_bronze_ingestion_olist.ipynb
- 02_silver_transformations_olist.ipynb
- 03_gold_marts_olist.ipynb
5. (Optional) Set up a Databricks Job for scheduled execution.
6. Connect Power BI to Gold tables to create dashboards.

# Key Skills Demonstrated
- PySpark data processing
- Delta Lake architecture
- Medallion design (Bronze / Silver / Gold)
- Dimensional modeling (Kimball)
- Data cleaning, conformance, and enrichment
- Orchestration with Databricks Jobs
- BI consumption via Power BI
