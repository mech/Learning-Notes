# Database Design

## Models

```
IBM IMS               Many-to-one
One-to-many           Many-to-many
document structure    solution
Tree-structure

Hierarchical Model -> Network Model    ->
                      Relational Model
```

> You can read a particular row by designating some columns as a key and matching on those.

* Document Model - Good locality. Schema flexibility.
* Relational Model - Support for joins, many-to-one and many-to-many relationships.

> If the data in your application has a document-like structure (i.e. a tree of one-to-many relationships, where typically the entire tree is loaded at once), then it's probably a good idea to use a document model. The relational technique of shredding - splitting a document-like structure into multiple tables (like positions, education and contact_info) - can lead to cumbersome schemas and unnecessarily complicated application code.

The poor support for joins in document databases may or may not be a problem, depending on the application. For example, many-to-many relationships may never be needed in an analytics application that uses a document database to record which events occurred at which time.

It's not possible to say in general which data model leads to simpler application code; it depends on the kinds of relationships that exist between data items. For highly interconnected data, the document model is awkward, the relational model is acceptable, and graph models are the most natural.