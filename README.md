# Data Engineering Nanodegree - Data Lake

On this project, we were requested to build a data ingestion pipeline for a number of JSON files provided on a S3 bucket along with the processing in Spark and the data loading into S3 parquet files. Some data manipulation was requested in order to create the parquet files with the same structure we've seen on the previous sessions.

## Project Execution
The right order to the execute this project is:
1. `etl.py`

The scripts must be executed on this order in order to correctly finish the processing. The script `etl.py` reads the JSON files, executes the data manipulation using Spark and save the data back on S3 as parquet files.

## Files Structure
### `etl.py`
This is the script that executes the ETL job logic itself. Its job is to load the JSON files into staging tables and then process the data into dimension and fact tables. The following functions can be found on the script.

`create_spark_session()` creates the Spark Session where the data will be processed. 

`process_song_data(spark, input_data, output_data)` reads the song data from S3 bucket and process the data in order to create the tables `songs` and `artists` according to the requirements. Once the processing is finished the tables are uploaded back to S3 but as parquet files.

`process_log_data(spark, input_data, output_data)` reads logs data from S3 and process the data to create the tables `users`, `times` and `songplays`. It also saves the tables as parquet files back to S3.

`main()` is entry function and sets how the process occurs when the script is executed. The scope here is to connect to the the cluster according to the configuration defined on `aws/credentials.cfg`, set `input_data` and `output_data` variables and call the functions `process_song_data` and `process_log_data`.