# Graphing

* Forward decay
* T-digest
* HdrHistogram

> Beware that averaging percentiles, e.g., to reduce the time resolution or to combine data from several machines, is mathematically meaningless - the right way of aggregating response time data is to add the histograms.

* [Don't use Timers with exponentially-decaying reservoirs in Graphite](http://taint.org/2014/01/16/145944a.html)

## Time Series

* [Open Source Time Series DB Comparison](https://docs.google.com/spreadsheets/d/1sMQe9oOKhMhIVw9WmuCEWdPtAoccJ4a-IuZv4fXDHxM/edit#gid=0)
* [InfluxDB](https://www.influxdata.com/)
* [Time-Series Database Requirements](https://www.xaprb.com/blog/2014/06/08/time-series-database-requirements/)
* [Schema Design for Time Series Data in MongoDB](https://www.mongodb.com/blog/post/schema-design-for-time-series-data-in-mongodb)
* [When Boring is Awesome: Building a scalable time-series database on PostgreSQL](https://blog.timescale.com/when-boring-is-awesome-building-a-scalable-time-series-database-on-postgresql-2900ea453ee2)
* [Square Cube](https://square.github.io/cube/)
* [Storing Time Series in PostgreSQL Efficiently](https://grisha.org/blog/2015/09/23/storing-time-series-in-postgresql-efficiently/)
* [What DB to use for huge time series](https://news.ycombinator.com/item?id=8368509)
* [Thoughts on Time-series Databases](http://jmoiron.net/blog/thoughts-on-timeseries-databases/)
* Resampling into time resolutions different from the storage resolution.
* Multi-tenancy. Some customers want to know their data is separate from other customers' data.

Immutable, large in volume, ordered by time, and is primarily aggregated for access.

There are a number of use cases that involve analyzing this history to better predict what may happen in the future or to establish **operational thresholds** for the system.

```js
// Store multiple readings (per day) in a single document
// If we have 30 recruiters with 31 days per month,
// then we will have 12,000 records per year

{
  work_month: "2017/4/1",
  recruiter_id: 51,
  type: "idle_jobs",
  values: {
    1: 0,
    2: 1,
    3: 0,
    ...
    31: 4
  }
}
```