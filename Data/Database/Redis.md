# Redis

* Started in 2009 by Salvatore Sanfilippo
* Allows different eviction policies beyond LRU (Least Recently Used) and LFU (Least Frequently Used - Redis 4.0)
* [redis-rb 4.0 support](https://github.com/rails/rails/pull/30748)

If you are using `redis-store` with Rails, consider using the `redis-rails` gem instead.

In addition to `redis-store`, there's a new Redis gem called `readthis` which show potential.

```ruby
# Use for ActionCable also
gem 'redis'

# Provide :redis_store
# May not be needed in Rails 5.2
gem 'redis-rails'

# Sidekiq recommend against using namespaces
gem 'redis-namespace'

# Or using the newer gem
gem 'readthis'
gem 'hiredis'

# You do not need to do the require if using Rails 5.2 since
# Rails will load redis/connection/hiredis for you
gem 'redis', '~> 3.0', require: ['redis', 'redis/connection/hiredis']
```

## Eviction

* By default Redis doesn't expire key when it hits max memory.
* Default policy for Azure Redis is **volitile-lru**, which means that only keys that have an expiration value will be considered for eviction. If no keys have an expiration value, then the system won't evict any keys and clients will get out of memory.
* You may want to consider **allkeys-lru**
* So to be safe, always set expiration value

## Persistence

* Redis is an In-Memory data store. Data loss can occur.
* Redis provides 3: RDB, AOF and both
* [Doc on persistence](https://redis.io/topics/persistence)
* [Setting up Redis for Production Environment](https://blog.sensible.io/2013/08/20/setting-up-redis-for-production-environment.html)

```
# RDB - Good for caching
# /var/lib/redis/dump.rdb
# Dump every 15 min = 900 seconds if at least 1 key changed
save 900 1

# AOF (Append Only File) - Good for Sidekiq background job
# /var/lib/redis/appendonly.aof
# Write to the log for all incoming write operations
appendonly yes

# Slow, but safest!
appendfsync always

# Compromise
appendfsync everysec
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

You can monkey-patch to delete key if it is nil or an empty array.

See https://github.com/rails/rails/issues/14075

```ruby
module CacheRealizer
  def realize(key, *args, &block)
    fetch(key, *args, &block).tap do |result|
      delete(key) if result.nil?
    end
  end
end

Rails.cache.extend(CacheRealizer)
```

## Rack::Cache

If you are not using Nginx, you can get some of the same benefits using `Rack::Cache`, which is a reverse proxy cache implemented as a Rack middleware. It is not as fast as an optimized web server like Nginx.

* [Speed up Rails with Nginx's Reverse Proxy Cache](https://mattbrictson.com/nginx-reverse-proxy-cache)

## Note on Cache

Use dedicated instance for caching and Sidekiq. Do not mix them together. Use Docker for 2 instances.

* [The Complete Guide to Rails Caching](https://www.speedshop.co/2015/07/15/the-complete-guide-to-rails-caching.html)
* [Optimizing Redis Usage For Caching](http://sorentwo.com/2015/07/27/optimizing-redis-usage-for-caching.html)
* [Caching GraphQL queries with GraphQL-ruby and Rails](http://mgiroux.me/2016/graphql-query-caching-with-rails/)
* [Using Redis as an LRU cache](https://redis.io/topics/lru-cache)

---

* Don't cache anything that takes less than 10-20ms to generate by itself.
* Network access to Redis host may have 50ms latency so it may not worth it.
* Use LRURedux or MemoryStore which are faster.

## redis-cli

```
▶ redis-cli --version

// See config variables
▶ redis-cli INFO

// See how many databases you have
▶ redis-cli INFO keyspace

// Timeout errors
▶ redis-cli --latency localhost

▶ redis-cli --bigkeys
```

```
▶ redis-cli -n 2

redis> CONFIG GET databases
redis> KEYS *
```

## redis.conf

* [Best Practices for Azure Redis](https://gist.github.com/JonCole/925630df72be1351b21440625ff2671f)

If you use Redis for Cache and Sidekiq, use 2 separate instances.

```
maxmemory-policy noeviction
```

## Rails

* [Pull request 31134 to add `:redis_cache_store`](https://github.com/rails/rails/pull/31134)

```ruby
config.cache_store = :redis_cache_store, { driver: :hiredis, url: 'redis://localhost:6379/0' }

# Find all the keys
Rails.cache.redis.keys
```

## Sidekiq

* [What is Sidekiq server and client?](https://github.com/mperham/sidekiq/issues/638)

## Monitoring

* [Healthcheck?](https://github.com/docker-library/healthcheck/blob/master/redis/docker-healthcheck)
* [redis-stat](https://github.com/junegunn/redis-stat)
* [How to Monitor Redis](https://blog.serverdensity.com/monitor-redis/)


