# Homework-3
I manually upload yellow taxi data into a GCS bucket
Then I imported the 6 dataset into bigquery and finally I build the whole 2024 dataset by UNION ALL the 6 ones

## Question 1
Just run `COUNT(*) FROM yellow_tripdata_2024`

Answer: 20,332,093 rows

## Question 2
For the external table, BigQuery would likely read the metadata from the parquet table stored in GCS
Otherwise, it will requires some computation depending lenght size

Answer: 0 MB for the External Table and 155.12 MB for the Materialized Table

## Question 3
The answer contains in itself the good explanation.
Answer: 1) BigQuery is a columnar database, and it only scans the specific columns requested in the query. Querying two columns (PULocationID, DOLocationID) requires reading more data than querying one column (PULocationID), leading to a higher estimated number of bytes processed.

## Question 4
Just run `COUNT(*) FROM yellow_tripdata_2024 WHERE fare_amount = 0`
ANSWER: 8333

## Question 5
First we cannot build to partion.
Second, AS we always run time filter, the best strategy is to divide the whole dataset into smaller one based on the filterer datetime
Cluster by Vendor Id is usefull so it will store the data with Vendor ID sorted

Answer: Partition by tpep_dropoff_datetime and Cluster on VendorID

## Question 6

I run `SELECT DISTINCT(VendorID) FROM table
WHERE tpep_dropoff_datetime >= '2024-03-01'
  AND tpep_dropoff_datetime <= '2024-03-16'`
For both the table, and the closest answer is 310.24 MB for non-partitioned table and 26.84 MB for the partitioned table

## Question 7
Answer: GCS

## Question 8
Answer False



