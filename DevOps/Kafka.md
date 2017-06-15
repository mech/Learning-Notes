# Kafka

Kafka does not do data processing or transforming. It basically is a logger to produce and consume messages.

* [Turning the database inside out with Apache Samza - Martin Kleppmann](https://www.youtube.com/watch?v=fU9hR3kiOK0)

## Database Locking

One of Kafka's main job is to alleviate database locking when you stream too much data too frequently to your main database.

## Offset

* Automatic or manual offset management
* Caught up with your offset

## Compaction

## LeaderNotAvailable

Looping and dropping messages

```
fetch.message.max.bytes
replica.fetch.max.bytes
```

## Videos

* [Processing Streaming Data at a Large Scale with Kafka](https://www.youtube.com/watch?v=-NMDqqW1uCE)