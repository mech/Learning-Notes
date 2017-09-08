# GraphQL

* [**GraphQL Specification**](https://facebook.github.io/graphql/)
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

GraphQL is a query language for APIs - not databases. It describe the data that you need, rather than HOW to get the data.

GraphQL is basically:

* Types
* Resolvers
* Query Composition - the parent component can gather up the child query and compose it into one single query request

```js
// Query Composition
// This parent component will render FriendListItem
// child component, so its query also need to be composed
// of child query
var FriendList = React.createClass({
  statics: {
    queries: {
      viewer: function() {
        return graphql`
          Viewer {
            friends {
              ${FriendListItem.getQuery('user')}
            }
          }
        `
      }
    }
  },
  
  render() {
    return (
      <div>
        {
          this.props.viewer.friends.map(user => <FriendListItem user={user}>)
        }
      </div>
    )
  }
})
```

GraphQL Documents are full of named things:

* Operations
* Fields - Conceptually a function with arguments and return values
* Arguments
* Directives
* Fragments (FragmentSpread, InlineFragment)
* Variables

You shouldn't need to restructure your data model; the whole point of GraphQL is to **abstract away implementation details** of data storage and express it in a natural, expressive, product-centric way.

```python
def graphql(request):
  schema = graphene.Schema(
    query=Query
  )

# Yelp expose business and search lookup
class Query(graphene.ObjectType):
  business = graphene.Field(
    Business,
    alias=graphene.String(),
  )
  
  search = graphene.Field(
    Businesses,
    term=graphene.String(),
    location=graphene.String(),
    # ...
  )
```

## What's Wrong with REST

* Fetching complicated object graphs (i.e. associations) get unwieldy quick
* REST's reliance on URL forces the use of incongruent query params to dynamically interact with resources
* Alternative is to keep resources simple and force multiple HTTP requests which lead to poor performance and over-fetching
* Weak-typing means little way of machine-readable metadata
* Endpoint creep
* Tight coupling between what the client want and what the server will provide. What shape of data do you want? Frontend developer will need to poke at server developer just to change the data shape.
* REST APIs have shown to be too inflexible to keep up with the rapidly changing requirements of the clients that access them.
* Proliferation of endpoints
* If strictly RESTful, too much network traffic

Compare to GraphQL, the steps in REST are:

1. Construct HTTP request using `fetch`
2. Receive and parse server response using `JSON.parse()`
3. Handle server errors
4. Store data locally
5. Display data in UI

With GraphQL, you just need to declare your data requirement and use Relay/Apollo to do the fetching/pagination/updating of UI.

## Authentication, Authorization, Caching

You don't do all these thing in GraphQL. GraphQL is designed to be a thin interface on top of these layers.

GraphQL should sit on top of your authentication system which is not coupled to GraphQL.

* Authentication should be with the HTTP layer
* Authorization should be with the Business Logic layer
* Do not put authorization logic at GraphQL layer
* Do not put business logic in the GraphQL layer

If you put authorization logic into your GraphQL, you won't be able to swap from REST to RPC or GraphQL. You also have a hard time to test for it.

## N+1 Problem

* Using Ruby Fibre to solve N+1 problem innately? See Airbnb Graphist. Fibre will block until doing all aggregation.
* N+1 is a under-fetching problem

## Thinking in Graphs

Think in graphs, not endpoints.

* [Thinking in Graphs](http://graphql.org/learn/thinking-in-graphs/)
* **Hierarchical** - Most product development involves the creation and manipulation of view hierarchies. To achieve congruence with the structure of these applications, a GraphQL query itself is a hierarchical set of fields. The query is shaped just like the data it returns. It is natural way for product engineers to describe data requirements.

## Design Your Schema

With SDL (Schema Definition Language). The schema tells the server what queries clients are allowed to make, and how different types are related.

```js
type Author {}
type Post {}

type Query {
  getAuthor(id: Int): Author
  getPostsByTitle(title: String): [Post]
}

schema {
  query: Query
}
```

* Domain-specific - DDD - Domain Modeling - Ubiquitous language
* Security concern? Some schema not to be exposed by others.
* Specify your **Response Shape**
* Think in graphs, not endpoints
* Describe the data, not the view

```js
// Do not model it based on UI view
// Image next time they want a new bigger image, then
// you need to add attachmentBigImage
storyAttachment {
  productID
  attachmentTitle
  attachmentImage
  attachmentSubtitle
}

// Instead, just model the data as you would
storyAttachment {
  product {
    id
    name
    image(size: 80)
  }
  upsellMessage
}
```

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

**Declarative API** - Don't worry about HOW the data is fetched. Or even WHEN it is fetched. The framework orchestrates the data-fetching.

* [Learn Relay](https://www.learnrelay.org/)
* GQL queries are co-located with the component with Relay Container Component
* Co-locate data fetching and rendering
* Intelligently aggregates queries so we don't over-fetch
* [#1369 - New Relay APIs](https://github.com/facebook/relay/issues/1369)
* Since Relay holds a central store, it is not compatible with Redux
* Node
* Fragment
* Pagination is part of the standard
* [Relay Modern example - Next.js](https://github.com/zeit/next.js/issues/1757)

Relay has 2 join models (the edge/connection paradigm):

1. Connection - keeps pagination data
2. Edge - wraps a cursor

Everything is nodes and edges in a graph.

## Fragments

Fragments are the primary unit of composition in GraphQL. It allow for the reuse of common repeated selections of fields, reducing duplicated text in the document.

Fragments are a common unit of composition allowing for query reuse.

The composition of all GraphQL fragments equals the total data requirements of the app.

## Static Queries

## Data Loader

Please don't do REST API backing your GraphQL. It will be damn slow. Always use some variants of Data Loader.

* [graphql-batch for Ruby, sort of like DataLoader](https://github.com/Shopify/graphql-batch)
* [DataLoader - Source code walkthrough by Lee Byron](https://www.youtube.com/watch?v=OQTnXNCDywA)
* [Ruby BatchLoader](https://engineering.universe.com/batching-a-powerful-way-to-solve-n-1-queries-every-rubyist-should-know-24e20c6e7b94)

## Edges and Connection

Ability to traverse edges or connections, 1-to-many relationships. 

## Pagination

* [Understanding pagination: REST, GraphQL, and Relay](https://dev-blog.apollodata.com/understanding-pagination-rest-graphql-and-relay-b10f835549e7)

Instead of using literal page numbers, idiomatic GraphQL uses opaque strings called **cursors**. Cursors are more resilient to real-time changes to your data, which might lead to duplicates in simple page-based systems.

## Rails

* [Building a full on GraphQL app](https://medium.com/ryancollinsio/building-a-full-on-graphql-app-b261f6cfea93)
* [How to Implement a GraphQL API in Rails](https://dzone.com/articles/how-to-implement-a-graphql-api-in-rails-via-codesh)
* [GraphQL + Relay Modern + Rails](https://collectiveidea.com/blog/archives/2017/08/03/graphql-relay-modern-rails)
* [Caching GraphQL queries with GraphQL-ruby and Rails](http://mgiroux.me/2016/graphql-query-caching-with-rails/)
* [graphql-ruby-demo](https://github.com/rmosolgo/graphql-ruby-demo)

## Resolvers

* Resolve functions are like little routers.
* Each field in the query corresponds to a resolve() function
* ALL resolvers are called. Query is traversed field by field, executing "resolves" for each field.
* Complexity is pushed to the server-side resolvers where powerful machines can take care of the heavy computation work and caching
* [How is query executed?](https://dev-blog.apollodata.com/graphql-explained-5844742f195e)

Server developer can focus on **describing the data available** rather than implementing and optimizing specific endpoints.

## Subscription

* [subscriptions-transport-ws](https://github.com/apollographql/subscriptions-transport-ws)
* [graphql-redis-subscriptions](https://github.com/davidyaha/graphql-redis-subscriptions)

## IDE Support

* [graphql-language-service](https://github.com/graphql/graphql-language-service)

## Videos

* [Lessons from 4 Years of GraphQL](https://www.youtube.com/watch?v=zVNrqo9XGOs)
* [High Performance GraphQL - DataLoader](https://www.youtube.com/watch?v=c35bj1AT3X8)
* [Using Apollo with ReactJS and GraphQL - SingaporeJS](https://www.youtube.com/watch?v=JCBVrE59yAI)