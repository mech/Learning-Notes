# Postgres

* [PostgreSQL Exercises](https://pgexercises.com/)
* [Our Postgres Infrastructure](http://blog.honeybadger.io/our-postgres-infrastructure/)
* [Introduction to PostgreSQL physical storage](http://rachbelaid.com/introduction-to-postgres-physical-storage/)
* [Chapter 66. Database Physical Storage](https://www.postgresql.org/docs/10/static/storage.html)
* [Postgres at Any Scale](https://www.youtube.com/watch?v=_wU2dglywAU)
* [Citus - For large Postgres](https://www.citusdata.com/)

```
▶ \x auto
```

## Tuning

* If you need more than 500 connections, use PGBouncer.

## EXPLAIN

* [Explaining the unexplainable](https://www.depesz.com/2013/05/09/explaining-the-unexplainable-part-3)
* [explain.depesz.com - Postgres explain analyze made readable](https://explain.depesz.com/)
* [Distinguishing Access and Filter-Predicates](http://use-the-index-luke.com/sql/explain-plan/postgresql/filter-predicates)

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

## Array

* [Postgres, the Good Parts: Arrays](http://blog.ryankelly.us/2016/08/21/postgres-the-good-parts-arrays.html)

## JSON

## Range

* tstzrange


## PL/V8

* [JavaScript in your Postgres](https://blog.heroku.com/javascript_in_your_postgres)

## Backup

* pg_dump is good for logical backup with less than 100GB of data
* Once you reached data that can't fit into RAM, you need to use physical backup like [WAL-E](https://github.com/wal-e/wal-e)
* [3 Methods of backing up Postgres](https://www.urbackup.org/backup_postgresql.html)