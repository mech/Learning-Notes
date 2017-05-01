# GraphQL

* [Artsy's GraphQL for Mobile](https://artsy.github.io/blog/2016/06/19/graphql-for-mobile/)
* [ReactQL](https://reactql.org/)
* [graphql-voyager](https://github.com/APIs-guru/graphql-voyager)
* [DataLoader](https://github.com/facebook/dataloader)

## What's Wrong with REST

* Fetching complicated object graphs (i.e. associations) get unwieldy quick
* REST's reliance on URL forces the use of incongruent query params to dynamically interact with resources
* Alternative is to keep resources simple and force multiple HTTP requests which lead to poor performance and over-fetching
* Weak-typing means little way of machine-readable metadata

## Thinking in Graphs

* [Thinking in Graphs](http://graphql.org/learn/thinking-in-graphs/)
* **Hierarchical** - Most product development involves the creation and manipulation of view hierarchies. To achieve congruence with the structure of these applications, a GraphQL query itself is a hierarchical set of fields. The query is shaped just like the data it returns. It is natural way for product engineers to describe data requirements.

## Design Your Schema

Schema is GraphQL's killer feature.

```ruby
ShopType = ObjectType.define do
  name 'Shop'
  description 'An awesome shop!'
  
  field :name, types.String, "The shops's name"
  field :currency, !types.Int # non-null field
  field :products, types[ProductType]
end
```

## Relay

* [Learn Relay](https://www.learnrelay.org/)

## Data Loader

* [graphql-batch for Ruby, sort of like DataLoader](https://github.com/Shopify/graphql-batch)

## Videos

* [Lessons from 4 Years of GraphQL](https://www.youtube.com/watch?v=zVNrqo9XGOs)
* [High Performance GraphQL - DataLoader](https://www.youtube.com/watch?v=c35bj1AT3X8)