# bricks_breaks_project

# Spotify Data Pipeline (End-to-End)

## Project Overview
This project implements a scalable ETL (Extract, Transform, Load) pipeline using Databricks and PySpark. It ingests raw Spotify music data, validates quality, optimizes storage layout, and creates an enriched "Silver" dataset ready for Machine Learning tasks.

## Architecture
The pipeline follows the **Medallion Architecture**:
1. **Bronze Layer:** Raw data ingestion with schema enforcement and error handling.
2. **Quarantine:** Automatic isolation of corrupt records.
3. **Silver Layer:** Cleaned, deduplicated, and enriched data partitioned by Genre.

## Dataset
* **Source:** [Kaggle Spotify Tracks Dataset](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset)
* **Format:** CSV (Batch)

## Prerequisites
* Databricks Runtime 12.2 LTS or higher (Spark 3.3+).
* Access to `default` database (Hive Metastore or Unity Catalog).
* Source file uploaded to `/Workspace/.../data/dataset.csv` (or DBFS).

## Project Structure
* `1_data_ingestion`: Reads CSV, handles errors, writes to Bronze.
* `2_data_storage`: Repartitions Bronze data by `track_genre` and runs `OPTIMIZE`.
* `3_data_processingT Removes duplicates, handles nulls, adds features, writes to Silver.

## Execution Instructions
### Manual Run
1. Open and run `1_data_ingestion`.
2. Open and run `2_data_storage`.
3. Open and run `3_data_processing`.

### Automated Run (Databricks Jobs)
1. Go to **Workflows** -> **Jobs**.
2. Select **"Spotify_end_to_end_pipeline"**.
3. Click **Run Now**.
4. Monitor progress in the "Runs" tab.