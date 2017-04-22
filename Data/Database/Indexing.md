# Indexing

* [Using indexes in rails: Index your associations](https://tomafro.net/2009/08/using-indexes-in-rails-index-your-associations)

```
EXPLAIN select * from conversations where lang = 'en' order by created_at DESC;
```

If you only index `lang` and not `created_at`, it will still be slow. The `lang` is using the index, but the ordering is using filesort which ultimately negate the gain. If you add a separate index to `created_at`, the result is still the same because MySQL can only use one index per table in a query. This is where [**indexing multiple columns**](https://tomafro.net/2009/08/using-indexes-in-rails-choosing-additional-indexes) comes in.

## Concurrent Indexing

* [Problems with concurrent Postgres indexes](https://medium.com/carwow-product-engineering/problems-with-concurrent-postgres-indexes-and-how-to-solve-them-c57f7656c852)

## Secondary Index

## Clustered and Non-Clustered Index

## Multi-dimensional Index

An interesting idea is that multi-dimensional indexes are not just for geographic locations. For example, on an e-commerce website you could use a three-dimensional index on the dimensions (red, green, blue) to search for products in a certain range of colors, or in a database of weather observations you could have a two-dimensional index on (date, temperature) in order to efficiently search for all the observations during the year 2013 where the temperature was between 25 and 30°C. With a one-dimensional index, you would have to either scan over all the records from 2013 (regardless of temperature) and then filter them by temperature, or vice versa. A 2D index could narrow down by timestamp and temperature simultaneously. This technique is used by HyperDex.