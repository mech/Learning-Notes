# Postgres

* [PostgreSQL Exercises](https://pgexercises.com/)
* [Our Postgres Infrastructure](http://blog.honeybadger.io/our-postgres-infrastructure/)
* [Introduction to PostgreSQL physical storage](http://rachbelaid.com/introduction-to-postgres-physical-storage/)
* [Chapter 66. Database Physical Storage](https://www.postgresql.org/docs/10/static/storage.html)
* [Postgres at Any Scale](https://www.youtube.com/watch?v=_wU2dglywAU)
* [HypoPG - hypothetical indexes](https://github.com/dalibo/hypopg)

```
▶ \x auto
```

## Indexing

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

## EXPLAIN ANALYZE

* [Explaining the unexplainable](https://www.depesz.com/2013/05/09/explaining-the-unexplainable-part-3)
* [explain.depesz.com - Postgres explain analyze made readable](https://explain.depesz.com/)
* [Distinguishing Access and Filter-Predicates](http://use-the-index-luke.com/sql/explain-plan/postgresql/filter-predicates)
* [Postgres EXPLAIN Visualizer (Pev)](http://tatiyants.com/pev/#/plans/new)

## Lateral Join

* [Postgres powerful new join type: Lateral](https://blog.heapanalytics.com/postgresqls-powerful-new-join-type-lateral/)

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

* [Folding Postgres Window Functions into Rails](https://blog.codeship.com/folding-postgres-window-functions-into-rails/)
* [Modeling Postgres Common Table Expressions and Window Functions with Rails and ActiveRecord](http://blog.nrowegt.com/modeling-postgres-common-table-expressions-and-window-functions-with-rails-and-activerecord/)

The strength of window functions is not pagination, but analytical calculation.

## Partition

* [pg_partman](https://github.com/keithf4/pg_partman)
* [partitionable](https://github.com/pacuna/partitionable)

## Date and Time

* [Dealing With User Timezones in Postgres](http://idlehands.codes/dealing-with-timezones-in-postgres)
* [Dealing With Time Zones Using Rails and Postgres](http://brendankemp.com/essays/dealing-with-time-zones-using-rails-and-postgres/)
* [How to deal with timestamps?](https://www.depesz.com/2014/04/04/how-to-deal-with-timestamps/)

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

## Pagination

> offset pagination is broken and there are other ways to paginate

* [Five ways to paginate in Postgres, from the basic to the exotic](https://www.citusdata.com/blog/2016/03/30/five-ways-to-paginate/)
* [Build JSON API Responses With Postgres CTEs](https://58.185.193.190/fmi/xml/cnt/79126%20Microsoft%20Certificate%201.pdf?-db=particulars&-lay=particulars&-recid=89215&-field=document(1))

## PL/V8

* [JavaScript in your Postgres](https://blog.heroku.com/javascript_in_your_postgres)

## RAM

## Parallel Query

* 9.6 has Parallel Sequential Scan
* Parallel aggregate and parallel join

## Backup

* pg_dump is good for logical backup with less than 100GB of data
* Once you reached data that can't fit into RAM, you need to use physical backup like [WAL-E](https://github.com/wal-e/wal-e)
* [3 Methods of backing up Postgres](https://www.urbackup.org/backup_postgresql.html)
* [WAL-E - Continuous archiving for Postgres](https://github.com/wal-e/wal-e)