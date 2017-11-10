# Kafka

A high-throughput distributed messaging system rethought as a **distributed commit log**.

Kafka does not do data processing or transforming. It basically is a logger to produce and consume messages. It is a distributed commit log.

* Producers push and consumers pull
* No state held by broker
* Data movement
* Decoupled. Multiple data producers and consumers.
* Re-playable history - configurable time-to-live for messages
* Retains offsets
* Enable **Event Sourcing** - an architectural style to maintaining an application's state by capturing all changes as a sequence of time-ordered, immutable events.
* Message stay on disk when consumed, deletes on TTL or compaction. You can store message for days or weeks, it does not get lost after being consumed. You can therefore go back and replay or rerun things if you want.

---

* [Turning the database inside out with Apache Samza - Martin Kleppmann](https://www.youtube.com/watch?v=fU9hR3kiOK0)

## Leaders and Followers

* Followers don't serve client requests, their only job is to replicate messages from the leader and stay up to date with the most recent messages the leader has

## Jobline

* Event-driven
* Central nervous system
* Central hub
* True integration
* Real-time processing

## Terms

* Worker
* Work load
* Topic
* Queue
* PubSub
* Route
* Message

## Database Locking

One of Kafka's main job is to alleviate database locking when you stream too much data too frequently to your main database.

Decouple producers and consumers.

## Offset

* Automatic or manual offset management
* Caught up with your offset
* Allow consumer to maintain isolation and autonomy
* Allow consumer to read message at their own pace
* Retention period is 168 hours or 7 days and is configurable

## Compaction

## LeaderNotAvailable

Looping and dropping messages

```
fetch.message.max.bytes
replica.fetch.max.bytes
```

## Videos

* [Processing Streaming Data at a Large Scale with Kafka](https://www.youtube.com/watch?v=-NMDqqW1uCE)