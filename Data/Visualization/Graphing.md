# Graphing

* Forward decay
* T-digest
* HdrHistogram

> Beware that averaging percentiles, e.g., to reduce the time resolution or to combine data from several machines, is mathematically meaningless - the right way of aggregating response time data is to add the histograms.

* [Don't use Timers with exponentially-decaying reservoirs in Graphite](http://taint.org/2014/01/16/145944a.html)

## Time Series

* [Schema Design for Time Series Data in MongoDB](https://www.mongodb.com/blog/post/schema-design-for-time-series-data-in-mongodb)
* [When Boring is Awesome: Building a scalable time-series database on PostgreSQL](https://blog.timescale.com/when-boring-is-awesome-building-a-scalable-time-series-database-on-postgresql-2900ea453ee2)

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