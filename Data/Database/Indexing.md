# Indexing

Indexing is all about deciding which columns to add to an index and in which order and combination.

> The most important information for proper indexing is not the storage system config or hardware setup. The most important information for indexing is how the application queries the data (a.k.a the access path).

* [Using indexes in rails: Index your associations](https://tomafro.net/2009/08/using-indexes-in-rails-index-your-associations)

```sql
EXPLAIN SELECT * FROM conversations WHERE lang = 'en' ORDER BY created_at DESC;
```

If you only index `lang` and not `created_at`, it will still be slow. The `lang` is using the index, but the ordering is using filesort which ultimately negate the gain. If you add a separate index to `created_at`, the result is still the same because MySQL can only use one index per table in a query. This is where [**indexing multiple columns**](https://tomafro.net/2009/08/using-indexes-in-rails-choosing-additional-indexes) comes in.

* Avoid `LIKE` expressions with leading wildcards (e.g. `'%TERM'`)
* Index for equality first, then for ranges
* One index scan is faster than 2. So don't use 2 separate indexes.
* Write range queries for period, do this even for a single day.

## Unused or redundant indexes

Covering indexes.

## Types of Indexes

Note: `FullTEXT` are not for ordinary `WHERE` clause operations so B-Tree is still useful for some columns.

**MySQL**

* B-tree
* R-tree - Geospatial
* Hash indexes

**Postgres**

* B-tree
* GIN
* GiST
* BRIN

## B-Tree

Why use B-Tree. Keeping the index order without moving large amounts of data when doing INSERT, UPDATE and DELETE. Database combines 2 data structures to meet the challenge: a doubly linked list and a search tree.

* Tree nodes are sorted in order - because B-Trees store the indexed columns in order, searching for ranges of data is efficient.
* Helpful for ORDER_BY queries also

## Multi-Column Index

A.k.a Concatenated index, composite or combined index.

Column order is important. You want the first index column to always be useable for searching.

As much as possible avoid concatenated index and just use single-column index. It saves storage space and has better INSERT, UPDATE, DELETE performance.

## Concurrent Indexing

* [Problems with concurrent Postgres indexes](https://medium.com/carwow-product-engineering/problems-with-concurrent-postgres-indexes-and-how-to-solve-them-c57f7656c852)

## Secondary Index

## Clustered and Non-Clustered Index

## Multi-dimensional Index

An interesting idea is that multi-dimensional indexes are not just for geographic locations. For example, on an e-commerce website you could use a three-dimensional index on the dimensions (red, green, blue) to search for products in a certain range of colors, or in a database of weather observations you could have a two-dimensional index on (date, temperature) in order to efficiently search for all the observations during the year 2013 where the temperature was between 25 and 30°C. With a one-dimensional index, you would have to either scan over all the records from 2013 (regardless of temperature) and then filter them by temperature, or vice versa. A 2D index could narrow down by timestamp and temperature simultaneously. This technique is used by HyperDex.

## Selectivity and Cardinality

Should you index boolean column? No.

> Unevenly distributed status codes like "todo" and "done" are a good example. The number of "done" entries often exceeds the "todo" records by an order of magnitude. Using an index only makes sense when searching for "todo" entries in that case.

## Dynamic SQL

## Access and Filter Predicate

## Range Indexing

```sql
// Queries with 2 or more independent range conditions
// It is impossible to define a B-tree index that support this
// This is because B-tree is essentially a linked list and not
// a Bitmap. You are doing multi-dimensional query.
SELECT fname, lname, dob
FROM employees
WHERE lname < ? AND dob < ?
```

## Videos

* [The Secret Life of SQL: How to Optimize Database Performance](https://www.youtube.com/watch?v=BuDWWadCqIw)