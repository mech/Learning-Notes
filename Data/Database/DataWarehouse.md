# Data Warehouse

* [Dremel made simple with Parquet](https://blog.twitter.com/2013/dremel-made-simple-with-parquet)
* [Postgres-XL](http://www.postgres-xl.org/faq/)
* [active_reporting](https://github.com/t27duck/active_reporting)
* [ransack - Object-based searching](https://github.com/activerecord-hackery/ransack)
* [Processing Streaming Data at a Large Scale with Kafka](https://www.youtube.com/watch?v=-NMDqqW1uCE)
* [Should You Use a Rowstore or a Columnstore?](http://blog.memsql.com/should-you-use-a-rowstore-or-a-columnstore/)
* [ETL for Pros: Getting Data Into MongoDB](https://explore.mongodb.com/vidyard-all-players/andre-spiegel-2?jmp=twt)

In normal business data processing, a write typically correspond to a transaction taking place. It is interactive and support ad-hoc queries.

However, databases also started being increasingly used for data analytics, which has very different access patterns.

Analytic query needs to scan over huge datasets, only reading a few columns per record, and calculate aggregate rather than returning the raw data to the user.

## Design

* Ask yourself: What are you analyzing?
* Get into the habit of tracking everything, like NSA.
* Track any events as facts.

## Issues

* No ActiveRecord instances (less memory). When you show metrics, do not instantiate any AR records.
* Generic, uniformed data (Arrays of rows)
* Only get the information we care about

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

* Rowstores are better at random reads and random writes
* Columnstores are better at sequential reads and sequential writes

---

* Dimensional tables can benefits from rowstore since it is read more randomly and not sequentially

## Bitmap vs B-tree Index

LSM-trees are faster for writes, whereas B-trees are faster for reads.

B-tree index must write every piece of data at least twice: once for the write-ahead log, and once to the tree page itself (and perhaps again as pages are split).

Work well for low-cardinality columns (little distinct values like boolean True/False for example).

Bitmap is less efficient than B-tree whose data is frequently updated.

## Redshift

* Expensive
* [2X Your Redshift Speed With Sortkeys and Distkeys](https://www.periscopedata.com/blog/double-your-redshift-performance-with-the-right-sortkeys-and-distkeys.html)

## Star Schema - Dimensional Modeling

* [A Beginner's Guide to Data Engineering — Part II](https://medium.com/@rchang/a-beginners-guide-to-data-engineering-part-ii-47c4e7cbda71)

* **Fact** - represents the event that occur
* **Dimensions** - represent the who, what, where, when, how, and why of the event

## Videos

* [Reporting on Rails - ActiveRecord and ROLAP Working Together](https://www.youtube.com/watch?v=MczzCfTQGfU)


