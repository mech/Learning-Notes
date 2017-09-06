# GraphQL

* [**How to GraphQL**](https://www.howtographql.com/)
* [Artsy's GraphQL for Mobile](https://artsy.github.io/blog/2016/06/19/graphql-for-mobile/)
* [ReactQL](https://reactql.org/)
* [graphql-voyager](https://github.com/APIs-guru/graphql-voyager)
* [DataLoader](https://github.com/facebook/dataloader)
* [Relay/GraphQL Cheatsheet #1](https://medium.com/code-oil/relay-graphql-cheatsheet-1-78eb66421d77)
* [GraphQL vs REST](https://dev-blog.apollodata.com/graphql-vs-rest-5d425123e34b)
* [The Anatomy of a GraphQL Query](https://dev-blog.apollodata.com/the-anatomy-of-a-graphql-query-6dffa9e9e747)
* [Representing State in REST and GraphQL](https://philsturgeon.uk/api/2017/06/19/representing-state-in-rest-and-graphql/)
* [GraphQL & React tutorial (part 1/6)](https://blog.hichroma.com/graphql-react-tutorial-part-1-6-d0691af25858)
* [postgraphql](https://github.com/postgraphql/postgraphql)
* [GraphQL Tour: Interfaces and Unions](https://medium.com/the-graphqlhub/graphql-tour-interfaces-and-unions-7dd5be35de0d)
* [Coursera's journey to GraphQL](https://dev-blog.apollodata.com/courseras-journey-to-graphql-a5ad3b77f39a)

GraphQL is basically:

* Types
* Resolvers

## What's Wrong with REST

* Fetching complicated object graphs (i.e. associations) get unwieldy quick
* REST's reliance on URL forces the use of incongruent query params to dynamically interact with resources
* Alternative is to keep resources simple and force multiple HTTP requests which lead to poor performance and over-fetching
* Weak-typing means little way of machine-readable metadata
* Endpoint creep

## N+1 Problem

## Thinking in Graphs

* [Thinking in Graphs](http://graphql.org/learn/thinking-in-graphs/)
* **Hierarchical** - Most product development involves the creation and manipulation of view hierarchies. To achieve congruence with the structure of these applications, a GraphQL query itself is a hierarchical set of fields. The query is shaped just like the data it returns. It is natural way for product engineers to describe data requirements.

## Design Your Schema

Schema is GraphQL's killer feature. You don't have a "book endpoint" where you get at the resource. Instead you have a `Book` and `Author` types.

```js
type Book {
  id: ID
  title: String
}

type Author {
  id: ID
  name: String
}
```

```ruby
ShopType = ObjectType.define do
  name 'Shop'
  description 'An awesome shop!'
  
  field :name, types.String, "The shops's name"
  field :currency, !types.Int # non-null field
  field :products, types[ProductType]
end
```

## Data Graph - Nodes and Edges

* Be careful of N+1 problem with many edges

## Type

Under-fetching is actually a type error.

## Relay

* [Learn Relay](https://www.learnrelay.org/)

## Static Queries

## Data Loader

Please don't do REST API backing your GraphQL. It will be damn slow. Always use some variants of Data Loader.

* [graphql-batch for Ruby, sort of like DataLoader](https://github.com/Shopify/graphql-batch)
* [DataLoader - Source code walkthrough by Lee Byron](https://www.youtube.com/watch?v=OQTnXNCDywA)
* [Ruby BatchLoader](https://engineering.universe.com/batching-a-powerful-way-to-solve-n-1-queries-every-rubyist-should-know-24e20c6e7b94)

## Pagination

* [Understanding pagination: REST, GraphQL, and Relay](https://dev-blog.apollodata.com/understanding-pagination-rest-graphql-and-relay-b10f835549e7)

Instead of using literal page numbers, idiomatic GraphQL uses opaque strings called **cursors**. Cursors are more resilient to real-time changes to your data, which might lead to duplicates in simple page-based systems.

## Rails

* [Building a full on GraphQL app](https://medium.com/ryancollinsio/building-a-full-on-graphql-app-b261f6cfea93)
* [How to Implement a GraphQL API in Rails](https://dzone.com/articles/how-to-implement-a-graphql-api-in-rails-via-codesh)
* [GraphQL + Relay Modern + Rails](https://collectiveidea.com/blog/archives/2017/08/03/graphql-relay-modern-rails)
* [Caching GraphQL queries with GraphQL-ruby and Rails](http://mgiroux.me/2016/graphql-query-caching-with-rails/)

## Videos

* [Lessons from 4 Years of GraphQL](https://www.youtube.com/watch?v=zVNrqo9XGOs)
* [High Performance GraphQL - DataLoader](https://www.youtube.com/watch?v=c35bj1AT3X8)
* [Using Apollo with ReactJS and GraphQL - SingaporeJS](https://www.youtube.com/watch?v=JCBVrE59yAI)