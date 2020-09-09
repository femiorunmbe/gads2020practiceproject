# LAB: Google Cloud Fundamentals: Getting Started with BigQuery

## Objectives
In this lab, you learn how to perform the following tasks:

    1. Load data from Cloud Storage into BigQuery.
    2. Perform a query on the data in BigQuery.

## Steps
1. Load data from Cloud Storage into BigQuery.
  - Create Dataset

        bq --location=US mk -d --description "Logdata dataset" logdata
  
  - Create a new table and load data
  
        bq mk --external_table_definition= --autodetect@CSV=gs://cloud-training/gcpfci/access_log.csv \ logdata.accesslog
        
2. Perform a query on the data in BigQuery.
  - Perform a query on the data using the BigQuery web UI
  
        bq query "select int64_field_6 as hour, count(*) as hitcount from logdata.accesslog group by hour order by hour"
        
  - Perform a query on the data using the bq command
  
        bq query "select string_field_10 as request, count(*) as requestcount from logdata.accesslog group by request order by requestcount desc"
