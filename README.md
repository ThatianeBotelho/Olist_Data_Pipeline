# Olist_Data_Pipeline

  /data_raw/
    olist_orders_dataset.csv
    olist_order_items_dataset.csv
    ...
  /notebooks/
    01_bronze_ingestion_olist.ipynb
    02_silver_transformations_olist.ipynb
    03_gold_marts_olist.ipynb
  /src/
    config.py
    etl_bronze.py
    etl_silver.py
    etl_gold.py
    utils/
      io.py
      transformations.py
  /orchestration/
    databricks_job_olist.json
  /docs/
    architecture_olist_pipeline.png
    data_model_gold_olist.png
