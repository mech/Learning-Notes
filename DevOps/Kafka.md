# Kafka

Kafka does not do data processing or transforming. It basically is a logger to produce and consume messages. It is a distributed commit log.

* Data movement
* Decoupled. Multiple data producers and consumers.
* Re-playable history - configurable time-to-live for messages
* Retains offsets
* Enable **Event Sourcing** - an architectural style to maintaining an application's state by capturing all changes as a sequence of time-ordered, immutable events.

---

* [Turning the database inside out with Apache Samza - Martin Kleppmann](https://www.youtube.com/watch?v=fU9hR3kiOK0)

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