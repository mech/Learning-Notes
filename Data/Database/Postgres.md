# Postgres

* [PostgreSQL Exercises](https://pgexercises.com/)
* [Our Postgres Infrastructure](http://blog.honeybadger.io/our-postgres-infrastructure/)
* [Introduction to PostgreSQL physical storage](http://rachbelaid.com/introduction-to-postgres-physical-storage/)
* [Chapter 66. Database Physical Storage](https://www.postgresql.org/docs/10/static/storage.html)
* [Postgres at Any Scale](https://www.youtube.com/watch?v=_wU2dglywAU)
* [Citus - For large Postgres](https://www.citusdata.com/)
* [HypoPG - hypothetical indexes](https://github.com/dalibo/hypopg)

```
▶ \x auto
```

## Embrace Constraints

* NOT NULL
* CREATE UNIQUE INDEX

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

## Materialized Views

* [Speed up with Materialized Views on PostgreSQL and Rails](https://www.sitepoint.com/speed-up-with-materialized-views-on-postgresql-and-rails/)

## Window Functions

* [Folding Postgres Window Functions into Rails](https://blog.codeship.com/folding-postgres-window-functions-into-rails/)
* [Modeling Postgres Common Table Expressions and Window Functions with Rails and ActiveRecord](http://blog.nrowegt.com/modeling-postgres-common-table-expressions-and-window-functions-with-rails-and-activerecord/)

The strength of window functions is not pagination, but analytical calculation.

## Partition

* [pg_partman](https://github.com/keithf4/pg_partman)
* [partitionable](https://github.com/pacuna/partitionable)

## Date

```sql
AVG(sale.price) as average_price,
MAX(sale.price) as max_price,
MIN(sale.price) as min_price,
ROUND(AVG(EXTRACT(EPOCH FROM sale.completed_at) - EXTRACT(EPOCH FROM sale.created_at))) as average_sale_time
```

## Array

* [Postgres, the Good Parts: Arrays](http://blog.ryankelly.us/2016/08/21/postgres-the-good-parts-arrays.html)

## JSON

## Range

* tstzrange

## Pagination

> offset pagination is broken and there are other ways to paginate

* [Five ways to paginate in Postgres, from the basic to the exotic](https://www.citusdata.com/blog/2016/03/30/five-ways-to-paginate/)

## PL/V8

* [JavaScript in your Postgres](https://blog.heroku.com/javascript_in_your_postgres)

## Backup

* pg_dump is good for logical backup with less than 100GB of data
* Once you reached data that can't fit into RAM, you need to use physical backup like [WAL-E](https://github.com/wal-e/wal-e)
* [3 Methods of backing up Postgres](https://www.urbackup.org/backup_postgresql.html)