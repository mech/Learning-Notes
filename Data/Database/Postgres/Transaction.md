# Transaction and Concurrency Control

When two or more sessions try to access the same data at the same time. Concurrency control is how Postgres can allow efficient access for all sessions while maintaining strict data integrity.

MVCC is how Postgres manage concurrent access to data. Rather than using traditional locking mechanism, MVCC locks acquired for querying (reading) do not conflict with locks acquired for writing, so reading never blocks writing and writing never blocks reading.

It is a multiversion model, which means each SQL statement sees a snapshot of the data as it was some time ago.

MVCC generally provide better performance than explicit locks.

1. Make use of implicit MVCC locks (let Postgres do it's own thing)
2. Use application-defined advisory locks
3. Use explicit locks yourself (as last resort if MVCC does not give the desired behavior)

> Locking is the key to performance.

## Isolation Level

Interaction between concurrent transactions must occur in some kind of isolation level in order to address the following phenomena (which MUST NOT happen):

* Dirty read
* Nonrepeatable read
* Phantom read
* Serialization anomaly

Example: With an isolation level of "Read committed", "Repeatable read", and "Serializable", the phenomena of "Dirty read" is not possible and MUST NOT happen.

* **Read committed** - The default isolation level in Postgres. Only ever read data from committed transactions. Uncommitted changes (dirty read) will never be queried and use. For normal OLTP, read committed has various advantages because changes can be seen much earlier and the odds of unexpected errors are usually lower.
* **Repeatable read** - Snapshot data before the whole transaction began. Will use the same snapshot through the entire transaction. This level is especially important if you want to run reports. The first and last page of a report should always be consistent and operate on the same data. Therefore, the repeatable read is key to consistent reports.
* **Serializable** - Run serially, rather than concurrently.

