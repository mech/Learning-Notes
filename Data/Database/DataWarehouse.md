# Data Warehouse

* [Dremel made simple with Parquet](https://blog.twitter.com/2013/dremel-made-simple-with-parquet)

In normal business data processing, a write typically correspond to a transaction taking place. It is interactive and support ad-hoc queries.

However, databases also started being increasingly used for data analytics, which has very different access patterns.

Analytic query needs to scan over huge datasets, only reading a few columns per record, and calculate aggregate rather than returning the raw data to the user.

## Design

* Ask yourself: What are you analyzing?
* Get into the habit of tracking everything, like NSA.
* Track any events as facts.

## Products

* Teradata
* Vertica
* SAP HANA
* ParAccel
* Apache Hive
* Spark SQL
* Impala
* Presto
* Apache Drill

## Write vs Read Time

If your read is compute-intensive because you need to query a lot of places, you may want to do more work at write time to compute result ahead of time so you can do less at read time.

Warehouse systems need to be read-optimized as most workload consists of ad-hoc queries that touch large amounts of historical data.

## Bitmap vs B-tree Index

LSM-trees are faster for writes, whereas B-trees are faster for reads.

B-tree index must write every piece of data at least twice: once for the write-ahead log, and once to the tree page itself (and perhaps again as pages are split).

## Redshift

* Expensive
* [2X Your Redshift Speed With Sortkeys and Distkeys](https://www.periscopedata.com/blog/double-your-redshift-performance-with-the-right-sortkeys-and-distkeys.html)

## Star Schema - Dimensional Modeling

* **Fact** - represents the event that occur
* **Dimensions** - represent the who, what, where, when, how, and why of the event


