# Elasticsearch

Initially for full-text search and when Lucene got more powerful and capable, it can do much more like log analytic and aggregation. Elasticsearch is just a distributed version of Lucene.

## Index

One index for one resource. Like timesheets in one index, users in one index, etc.

If you have billion of timesheets to store and it reaches the physical limitation of the disk (> 1TB e.g.), you want to divide your index into multiple shards in different machine node.

Each index is a Lucene index and has a limit of 2,147,483,519 maximum number of documents.

## Shards

The number of primary shards cannot be changed later. You must determine your primary shards now. Not as bad as it sounds though, as you can add more replica shards for more read throughput. It is just the write that will suffer a bit.

Worst case you can re-index your data.

```
"settings": {
  "number_of_shards": 3,
  "number_of_replicas": 1
}
```

## Unassigned Shards (Red)

## Typeless API



```
▶ curl -XGET "172.16.78.129:9200/_cat/health?help"
▶ curl -XGET "172.16.78.129:9200/_cat/health?v"
▶ curl -XGET "172.16.78.129:9200/_cat/health?format=json&pretty"
```
