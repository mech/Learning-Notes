# Postgres

* [The Internals of PostgreSQL](http://www.interdb.jp/pg/)
* [PostgreSQL Exercises](https://pgexercises.com/)
* [Our Postgres Infrastructure](http://blog.honeybadger.io/our-postgres-infrastructure/)
* [Introduction to PostgreSQL physical storage](http://rachbelaid.com/introduction-to-postgres-physical-storage/)
* [Chapter 66. Database Physical Storage](https://www.postgresql.org/docs/10/static/storage.html)
* [Postgres at Any Scale](https://www.youtube.com/watch?v=_wU2dglywAU)
* [HypoPG - hypothetical indexes](https://github.com/dalibo/hypopg)
* [5 Things I wish my grandfather told me about ActiveRecord and Postgres](https://medium.com/carwow-product-engineering/5-things-i-wish-my-grandfather-told-me-about-activerecord-and-postgres-93416faa09e7)
* [My Top 10 Postgres Features and Tips for 2016](http://www.craigkerstiens.com/2015/12/29/my-postgres-top-10-for-2016/)
* [pg_cron: Run periodic jobs in PostgreSQL](https://www.citusdata.com/blog/2016/09/09/pgcron-run-periodic-jobs-in-postgres/)
* [Performance Tuning Queries in PostgreSQL](https://www.geekytidbits.com/performance-tuning-postgres/)
* [Debugging complex PostgreSQL queries with **pgdebug**](http://korban.net/posts/postgres/2017-09-18-debugging-complex-postgres-queries-with-pgdebug/)
* [The case against ORMs](http://korban.net/posts/postgres/2017-11-02-the-case-against-orms/)
* [Postgres Hidden Gems](http://www.craigkerstiens.com/2018/01/31/postgres-hidden-gems/)

```
▶ \x auto
```

```sql
// A faster way to write `WHERE id IN ($1, $2, $3)`
SELECT * from users WHERE id = ANY($1::int[])
```

## As a Job Queue

* [What is SKIP LOCKED for in PostgreSQL 9.5?](https://blog.2ndquadrant.com/what-is-select-skip-locked-for-in-postgresql-9-5/)
* [How we built a job queue with Postgres](https://blog.holistics.io/how-we-built-a-multi-tenant-job-queue-system-with-postgresql-ruby/)

## Constraints

* [Protect Your Data with PostgreSQL Constraints](http://nathanmlong.com/2016/01/protect-your-data-with-postgresql-constraints/)

## RBAC

* [Postgraphile - Postgres for GraphQL](https://www.graphile.org/postgraphile/introduction/)
* [Role-based grant system](https://www.postgresql.org/docs/9.6/static/user-manag.html)
* [RLS - Row-level security policies](https://www.postgresql.org/docs/9.6/static/ddl-rowsecurity.html)

## Rollup

* [Efficient rollup tables with HyperLogLog in Postgres](https://www.citusdata.com/blog/2017/06/30/efficient-rollup-with-hyperloglog-on-postgres/)

## Time-Series

* [Problems with PostgreSQL 10 for time-series data](https://blog.timescale.com/time-series-data-postgresql-10-vs-timescaledb-816ee808bac5)
* [Time Series Database Lectures - Fall 2017](http://db.cs.cmu.edu/seminar2017/)

## Indexing

* [Introducing Dexter, the Automatic Indexer for Postgres](https://medium.com/@ankane/introducing-dexter-the-automatic-indexer-for-postgres-5f8fa8b28f27)
* [How About Hypothetical Indexes ?](https://rjuju.github.io/postgresql/2015/07/02/how-about-hypothetical-indexes.html)
* Indexes add overhead to write operations like INSERT, UPDATE and DELETE. Because of this, you may not want to index write-heavy tables.
* [Index Columns for `LIKE` in PostgreSQL](https://niallburkley.com/blog/index-columns-for-like-in-postgres/)

**BRIN**

```sql
--- table with 100M rows
CREATE TABLE test_bitmap AS
  SELECT mod(i, 100.000) AS val
    FROM generate_series(1, 100.000.000) s(i);
CREATE INDEX test_btree_idx ON test_bitmap(val);
CREATE INDEX test_brin_idx ON test_bitmap USING brin(val);
```

```sql
CREATE EXTENSION IF NOT EXISTS "btree_gist";
CREATE INDEX ON dynos USING GiST (
  instance_id, tstzrange(started_at, stopped_at, '[]')
)
CREATE INDEX ON dynos (started_at)
CREATE INDEX ON dynos (stopped_at)

SELECT instance_id, started_at, stopped_at
FROM dynos
WHERE instance_id=453345
AND tstzrange(started_at, stopped_at, '[]') @> '2017-05-08 00:57:41'::timestamptz;
```

## Scaling

* [Citus - For large Postgres](https://www.citusdata.com/)
* [Postgres-XL](http://www.postgres-xl.org/)
* [Greenplum](http://greenplum.org/)
* [cstore_fdw - Columnar store for analytics with PostgreSQL](https://github.com/citusdata/cstore_fdw)

## Embrace Constraints

* NOT NULL
* CREATE UNIQUE INDEX
* Use check constraints with PLV8??

## Performance

Most single queries should be aiming for around a 1ms query time.

* [Expensive Query Dashboard](https://blog.heroku.com/expensive-query-speed-up-app)
* [Using Rack Mini Profiler to find and fix slow queries](https://schneems.com/2017/06/22/a-tale-of-slow-pagination/)

## UUID

* [A Brief History of the UUID](https://segment.com/blog/a-brief-history-of-the-uuid/)

## Tuning

* If you need more than 500 connections, use PGBouncer.

## EXPLAIN and EXPLAIN ANALYZE

* [Explaining the unexplainable](https://www.depesz.com/2013/05/09/explaining-the-unexplainable-part-3)
* [explain.depesz.com - Postgres explain analyze made readable](https://explain.depesz.com/)
* [Distinguishing Access and Filter-Predicates](http://use-the-index-luke.com/sql/explain-plan/postgresql/filter-predicates)
* [Postgres EXPLAIN Visualizer (Pev)](http://tatiyants.com/pev/#/plans/new)

## Lateral Join

* [Postgres powerful new join type: Lateral](https://blog.heapanalytics.com/postgresqls-powerful-new-join-type-lateral/)
* [PostgreSQL's LATERAL JOIN](https://medium.com/kkempin/postgresqls-lateral-join-bfd6bd0199df)

## SKIP LOCKED

* [PG Casts - The Skip Locked feature in Postgres 9.5](https://www.pgcasts.com/episodes/7/skip-locked/)
* Good for implementing queue?

## pg_tune

## Incidents to learn

* [Gitlab DB incident](https://about.gitlab.com/2017/02/01/gitlab-dot-com-database-incident/)

## Materialized/SQL Views

* [Speed up with Materialized Views on PostgreSQL and Rails](https://www.sitepoint.com/speed-up-with-materialized-views-on-postgresql-and-rails/)
* Essentially a caching system at the database
* Virtual table
* Providing roll-ups

## Window Functions

Unlike aggregate function like `COUNT()`, `SUM()`, `AVG()`, which operate on an entire table, Window Functions operate on a set of rows and return a single aggregated value for each row.

The rows retain their separate identities and the aggregated value is merely added to each row rather than grouped together.

* [Folding Postgres Window Functions into Rails](https://blog.codeship.com/folding-postgres-window-functions-into-rails/)
* [Modeling Postgres Common Table Expressions and Window Functions with Rails and ActiveRecord](http://blog.nrowegt.com/modeling-postgres-common-table-expressions-and-window-functions-with-rails-and-activerecord/)
* [Advanced SQL - window functions](http://mjk.space/advanced-sql-window-functions/)
* ANSI/ISO Standard SQL:2003
* ANSI/ISO Standard SQL:2008
* Microsoft SQL Server 2005 implemented (ROW_NUMBER, RANK, NTILE and DENSE_RANK functions only)
* SQL Server 2012 implemented the full range of functions finally
* MariaDB 10.2.0 implemented Window Functions finally
* MySQL 8 implemented Window Functions finally

The strength of window functions is not pagination, but **analytical calculation**.

The set of rows used for the calculation is called the "window" and will the entire dataset by default.

The `PARTITION BY` is employed to reduce the window to a particular group within the dataset.

## Partition

* [pg_partman](https://github.com/keithf4/pg_partman)
* [partitionable](https://github.com/pacuna/partitionable)

## Date and Time

* [Dealing With User Timezones in Postgres](http://idlehands.codes/dealing-with-timezones-in-postgres)
* [Dealing With Time Zones Using Rails and Postgres](http://brendankemp.com/essays/dealing-with-time-zones-using-rails-and-postgres/)
* [How to deal with timestamps?](https://www.depesz.com/2014/04/04/how-to-deal-with-timestamps/)
* [Working With Time in Postgres](http://www.craigkerstiens.com/2017/06/08/working-with-time-in-postgres/)
* [Better Date Manipulation in PostgreSQL Queries](https://robots.thoughtbot.com/better-date-manipulation-in-postgres-queries)

```sql
WHERE inserted_at
BETWEEN ('2016-12-21 00:00:00.000'::timestamp AT TIME ZONE u.timezone)
AND
        ('2016-12-21 23:59:59.999'::timestamp AT TIME ZONE u.timezone)
```

```sql
AVG(sale.price) as average_price,
MAX(sale.price) as max_price,
MIN(sale.price) as min_price,
ROUND(AVG(EXTRACT(EPOCH FROM sale.completed_at) - EXTRACT(EPOCH FROM sale.created_at))) as average_sale_time
```

## Array

* [Postgres, the Good Parts: Arrays](http://blog.ryankelly.us/2016/08/21/postgres-the-good-parts-arrays.html)

## JSONB

* 12 operators and 23 functions (as of 9.5)
* 2 different indexing methods
* Good for storing, but need to be replaced entirely for updates
* [How to convert json string to text?](https://stackoverflow.com/questions/27215216/postgres-how-to-convert-json-string-to-text/31757242#31757242)

## Range

* tstzrange

```sql
CREATE TABLE billings (
  formation_id    uuid      NOT NULL,
  validity_period tstzrange NOT NULL,
  price_per_month integer   NOT NULL
);

# Exclusion constraints
ALTER TABLE ONLY billings
ADD CONSTRAINT billings_excl
EXCLUDE USING gist (
  uuid_send(formation_id) WITH =,
  validity_period WITH &&
)
```

## ENUM

* Good for small unchanging constants like AWS regions

## Pagination - OFFSET vs Cursor/Keyset

> offset pagination is broken and there are other ways to paginate

* [Five ways to paginate in Postgres, from the basic to the exotic](https://www.citusdata.com/blog/2016/03/30/five-ways-to-paginate/)
* [Build JSON API Responses With Postgres CTEs](http://www.codedependant.net/2017/04/30/build-json-api-responses-postregres-with-cte/)
* [We need tool support for keyset pagination](http://use-the-index-luke.com/no-offset)
* [Pagination: You're (Probably) Doing It Wrong](https://coderwall.com/p/lkcaag/pagination-you-re-probably-doing-it-wrong)
* [We need tool support for keyset pagination](https://use-the-index-luke.com/no-offset)

## PL/V8

* [JavaScript in your Postgres](https://blog.heroku.com/javascript_in_your_postgres)

## RAM

## Parallel Query

* 9.6 has Parallel Sequential Scan
* Parallel aggregate and parallel join

## Full-Text Search

* [Postgres Text Search: Simple, Adequate](http://info.pagnis.in/blog/2017/06/18/postgres-text-search-simple-adequate/)
* [Implementing Multi-Table Full Text Search with Postgres in Rails](https://robots.thoughtbot.com/implementing-multi-table-full-text-search-with-postgres)

## Backup

* pg_dump is good for logical backup with less than 100GB of data
* Once you reached data that can't fit into RAM, you need to use physical backup like [WAL-E](https://github.com/wal-e/wal-e)
* [3 Methods of backing up Postgres](https://www.urbackup.org/backup_postgresql.html)
* [WAL-E - Continuous archiving for Postgres](https://github.com/wal-e/wal-e)

## Compression

* TOAST - Automatic Table Compression

## People

* [Craig Kerstiens](http://www.craigkerstiens.com/)

## Blog

* [PG Analyze blog](https://pganalyze.com/blog)
* [](https://brandur.org/articles)

## Videos

* [PostgresOpen](https://www.youtube.com/user/postgresopen)
* [dotScale 2017 - Marco Slot - Scaling out (Postgres)SQL](https://www.youtube.com/watch?v=xJghcPs0ibQ)
* [Skillsmatter's Postgres Videos](https://skillsmatter.com/explore?q=tag%3Apostgresql)

