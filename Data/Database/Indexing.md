# Indexing

* [Using indexes in rails: Index your associations](https://tomafro.net/2009/08/using-indexes-in-rails-index-your-associations)

```
EXPLAIN select * from conversations where lang = 'en' order by created_at DESC;
```

If you only index `lang` and not `created_at`, it will still be slow. The `lang` is using the index, but the ordering is using filesort which ultimately negate the gain. If you add a separate index to `created_at`, the result is still the same because MySQL can only use one index per table in a query. This is where [**indexing multiple columns**](https://tomafro.net/2009/08/using-indexes-in-rails-choosing-additional-indexes) comes in.

## Concurrent Indexing

* [Problems with concurrent Postgres indexes](https://medium.com/carwow-product-engineering/problems-with-concurrent-postgres-indexes-and-how-to-solve-them-c57f7656c852)
