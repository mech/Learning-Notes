# Redis

* Started in 2009 by Salvatore Sanfilippo
* Allows different eviction policies beyond LRU (Least Recently Used) and LFU (Least Frequently Used - Redis 4.0)
* [redis-rb 4.0 support](https://github.com/rails/rails/pull/30748)

If you are using `redis-store` with Rails, consider using the `redis-rails` gem instead.

In addition to `redis-store`, there's a new Redis gem called `readthis` which show potential.

```ruby
# Use for ActionCable also
gem 'redis'

# Better to use redis-rails than only redis-store
gem 'redis-rails'

# Namespace is always good to have
gem 'redis-namespace'

# Or using the newer gem
gem 'readthis'
gem 'hiredis'
gem 'redis', '~> 3.0', require: ['redis', 'redis/connection/hiredis']
```

## Persistence

* [Doc on persistence](https://redis.io/topics/persistence)

```
appendonly yes
appendfsync always
```

Run different Redis instances for Cache and Unified Log.

## Rate Limiting

* [redis-cell - rate limiting in Redis as a single command](https://github.com/brandur/redis-cell)

## As Kafka with Redis Stream

* [Redis Streams and the Unified Log](https://brandur.org/redis-streams)
* [Streams: a new general purpose data structure in Redis](http://antirez.com/news/114)

## Database

Appending a number between 0 and 15 will specify the redis database, which defaults to 0.

```
REDIS_URL=redis://localhost:6379/2
```

## Caching nil

It is possible but not recommended to cache `nil`. `fetch()` treat `nil` values as a cache miss and re-generate/re-cache the value.

## Rack::Cache

If you are not using Nginx, you can get some of the same benefits using `Rack::Cache`, which is a reverse proxy cache implemented as a Rack middleware. It is not as fast as an optimized web server like Nginx.

* [Speed up Rails with Nginx's Reverse Proxy Cache](https://mattbrictson.com/nginx-reverse-proxy-cache)

## Note on Cache

Use dedicated instance for caching and Sidekiq. Do not mix them together. Use Docker for 2 instances.

* [The Complete Guide to Rails Caching](https://www.speedshop.co/2015/07/15/the-complete-guide-to-rails-caching.html)
* [Optimizing Redis Usage For Caching](http://sorentwo.com/2015/07/27/optimizing-redis-usage-for-caching.html)
* [Caching GraphQL queries with GraphQL-ruby and Rails](http://mgiroux.me/2016/graphql-query-caching-with-rails/)

---

* Don't cache anything that takes less than 10-20ms to generate by itself.
* Network access to Redis host may have 50ms latency so it may not worth it.
* Use LRURedux or MemoryStore which are faster.

## redis-cli

```
// See config variables
▶ redis-cli INFO

// See how many databases you have
▶ redis-cli INFO keyspace

// Timeout errors
▶ redis-cli --latency localhost

▶ redis-cli --bigkeys
```

```
redis> CONFIG GET databases
redis> 
```

## redis.conf

If you use Redis for Cache and Sidekiq, use 2 separate instances.

```
maxmemory-policy noeviction
```

## Sidekiq

* [What is Sidekiq server and client?](https://github.com/mperham/sidekiq/issues/638)

