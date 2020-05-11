# Summary of project

Startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

In order to enable Sparkify to parse their data automated over S3 into Redshift, they decided to use Airflow to schedule and monitor their pipeline jobs.

# Files in the repository

* **[airflow](airflow)**: workspace folder storing the airflow DAGs and plugins used by the airflow server.
* **[airflow/dags/s3_to_redshift_dag.py](airflow/dags/s3_to_redshift_dag.py)**: "Main"-DAG written in Python containing all steps of the pipeline.
* **[airflow/plugins/operators/](airflow/plugins/operators)**: Folder containing such called operators which can be called inside an Airflow DAG. These are python classes to outsource and build generic functions as modules of the DAG.

# The required DAG

<img src="./images/airflow_dag.jpg?raw=true" width="800" />

# The database schema design and ETL pipeline.

In order to enable Sparkify to analyze their data, a Relational Database Schema was created, which can be filled with an ETL pipeline.

The so-called star scheme enables the company to view the user behaviour over several dimensions.
The fact table is used to store all user song activities that contain the category "NextSong". Using this table, the company can relate and analyze the dimensions users, songs, artists and time.

* **Fact Table**: songplays
* **Dimension Tables**: users, songs, artists and time.

# Dataset used

The data is queried from s3 buckets hosted at AWS

* **Song data**: ```s3://udacity-dend/song_data```
* **Log data**: ```s3://udacity-dend/log_data```

The first dataset is a subset of real data from the [Million Song Dataset](http://millionsongdataset.com/). Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. 

The second dataset consists of log files in JSON format generated by this event simulator based on the songs in the dataset above. These simulate app activity logs from an imaginary music streaming app based on configuration settings.
