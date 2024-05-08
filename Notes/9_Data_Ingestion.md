# Data Ingestion

## Data Ingestion - CSV

https://spark.apache.org/docs/latest/api/python/reference/index.html

https://spark.apache.org/docs/latest/api/python/index.html

### Data Ingestion Requirements
- Ingest 8 files into the data lake
- Ingested data must have the schema applied
- Ingested data must have audit columns
- Ingested data must be stored in columnar format - Parquet
- Must be able to analyse the ingested data via SQL
- Ingestion logic must be able to handle incremental load - data received for one race should be appended rather than replacing all data in the data lake

### ETL Data Processing

- In ETL Data processing, input data can be in files of various formats such as tables and real time streams
- Ingestion process reads data, transforms data including applying schema and fixing data quality, aggregations, and then writes data into output storage such as file store, databases, or streams
- Spark provides a DataFrameReader API,  DataFrame APIs to transform data, and a DataFrameWriter API to write data to output sources in a range of file formats

<img src="Docs/ingestion_overview.png">

### Ingest Circuits File CSV
- Read the CSV file using the spark Dataframe Reader API
- Specify Schema for the data
- Add ingestion date and race_timestamp columns
- Select only he required columns
- Rename columns
- write data to data lake as parquet


### Ingest Races File CSV
- Read the CSV file using the spark Dataframe Reader
- Specify Schema for the data (infer schema reads the data, infers schema, and applies the schema to the Dataframe which is inefficient - for large datasets it slows down reads and query times. Infer schema can be used in test or dev but in production when we have data that does not conform to expected data, we want our process to fail. Therefore specifying the schema is the best practice)
- Select only he required columns
- Rename columns
- Add ingestion date to the Dataframe
- write data to data lake as parquet - partition by race year using partition by. When data is written to ADLS storage, a folder will be created for each of the race years, this allows spark to read data of specific race years or partitions efficiently and process the data in parallel. Too many partitions can have an adverse effect in partition. Common partitions include date of data received, race_year, race_id (all data for a race in one partition)

### Ingest Races File JSON
- Read the JSON file using the spark Dataframe Reader
- Drop unwanted columns from the DataFrame
- Rename columns and add ingestion date
- Write output to parquet file


### Ingest Drivers File JSON
- Read the JSON file using the spark Dataframe Reader
- name object for driver is nested within another nested JSON object with forename and surname. Schema needs to read this nested data and fields need to be concatenated

### Ingest Results File Json

- Read the JSON file using the spark Dataframe Reader
- data is a single line JSON file with no nested objects with 25000 records to process
- Rename columns and add new columns
- Drop unwanted columns from the DataFrame
- Write output to parquet file

### Ingest Pitstops File JSON
- Read the JSON file using the spark Dataframe Reader
- data is a multi line JSON file where JSON objects are in multiple lines
- Rename columns and add new columns
- Write output to parquet file

### Ingest Laptimes Folder -  Multiple CSV files
- Read the CSV file using the spark Dataframe Reader
- data for laptimes is a folder which contains lap time data split into five separate files
- standard CSV file but does not contain a header as its split across files
- Rename columns and add new columns
- Write output to container in parquet file format


### Ingest Qualifying Folder -  Multiple JSON files
- Read the CSV file using the spark Dataframe Reader
- data to be processed is a set of multiple multi line JSON files as input
- qualifying folder contains qualifying data split into two JSON files
- Rename columns and add new columns
- Write output to container in parquet file format
