# Tools

* [Apache Airflow](https://airflow.apache.org/) - Monitor workflows as DAGs of tasks.
* [Apache Spark](https://spark.apache.org/) - Data processing without MapReduce. Overtake Hadoop Map Reduce. Spark can execute batch processing jobs 10 to 100 times faster than MapReduce.
* [Apache Flink](https://flink.apache.org/) - Overtake Spark's batch processing

## Spark

* In-memory data processing using RDD (Resilient Distributed Datasets)
* Batch processing - Micro-batch.
* Spark SQL for SQL queries
* GraphX for graph processing
* MLlib for machine learning
* Medium latency, high throughput

Capable of running on standalone mode (with S3), but many run on top of Hadoop (YARN, HDFS).

## Flink

> Life doesn't happen in batches...

What's the problem with "process-after-store" model? Unnecessary latencies between data generation and analysis and actions on the data as well as implicit assumption that the data is complete after a given period of time and can be used to make accurate predictions.

* In-memory data processing
* Stream processing - true streams. Treat stream input data as stream and not batch
* MRQL for SQL queries
* Spargel/Gelly for graph processing
* Flink ML for machine learning
* Good YARN citizen
* Low latency, high throughput