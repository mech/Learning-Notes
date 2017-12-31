# GraphQL

https://gramps-graphql.github.io/gramps-express/

> Finally! I can see my business domain - with GraphQL Voyager

* DDoS
* Are you leaking implementation details
* Protocol buffer? gRPC?
* Backend APIs are storage-centric
* Front-end APIs are product-centric


> Unapologetically view-based

Each component specifies the bit of data that it will need in the form of a **query fragment**, and the framework takes care of composing all of the fragments into a larger hierarchy that represents the entire query. Because all of this is centralized in the framework, even dealing with massive queries (ie. all the data your entire application needs to render a complex, nested view hierarchy) can be made efficient through caching, batching, re-use, and other means to reduce the size of queries.

> No need to transform into the shape that you need from REST endpoint. It is already on the correct shape.

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
* [GitHub's Platform Forum for GraphQL](https://platform.github.community/c/graphql-api)

React has view hierarchy. GraphQL has function hierarchy (fragments).

GraphQL is a query language for APIs - not databases. It describe the data that you need, rather than HOW to get the data.

GraphQL queries provide an efficient way to fetch data, even across multiple types. This results in a great abstraction layer on top of databases.

GraphQL is basically:

* Types
* Resolvers

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
  hello = graphene.String()
  
  def resolve_hello(self, info):
    return 'World'

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

REST is limited.

REST only contains the notion of resource - there is no notion of fields that you could use to restrict the response to only the details you need.

REST has resources and sub-resources. Most of the time, you need to fetch additional requests just to get the sub-resources.

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

* [A guide to authentication in GraphQL](https://dev-blog.apollodata.com/a-guide-to-authentication-in-graphql-e002a4039d1)
* [Facebook is using something like **Permission Queries**](https://blog.graph.cool/reinventing-authorization-graphql-permission-queries-f2bd041bcd76)
* [Crazy thinking](https://github.com/apollographql/graphql-tools/issues/313)
* [How Facebook do Authorization](https://www.youtube.com/watch?v=etax3aEe2dA)

You don't do all these thing in GraphQL. GraphQL is designed to be a thin interface on top of these layers.

GraphQL should sit on top of your authentication system which is not coupled to GraphQL.

* Authentication should be with the HTTP layer
* Authorization should be with the Business Logic layer
* Do not put authorization logic at GraphQL layer
* Do not put business logic in the GraphQL layer
* Free-form data traversing nature of GraphQL adds new access control challenges
* Can't rely on conventional status codes like REST. You can't say 10 field queries are 403 forbidden when there are at least 5 201 succeeded.

If you put authorization logic into your GraphQL, you won't be able to swap from REST to RPC or GraphQL. You also have a hard time to test for it.

---

1. Login using `/auth/token` endpoint
2. Send the token with your request to prove identity

## Validation and Masking Error

We need to mask server errors to client.

* [Validation and User Errors in GraphQL Mutations](https://medium.com/@tarkus/validation-and-user-errors-in-graphql-mutations-39ca79cd00bf)

## Error

* GraphQL is capable of representing partial success
* The request shouldn't blow up just because part of the request failed
* This make tracking success rate a little difficult as GraphQL nearly always return success 200 even if it did not fetch any data
* Track your error as GraphQL do not provide backtraces and line numbers

```js
// Form error can be query also
// Treat error as data also
mutation createUser {
  createUser(email: 'test@example.com') {
    user {
      id
      email
    }
    wasSuccessful
    userErrors {
      field
      message
    }
  }
}
```

### Context

* Once authentication with a separate endpoint, you simply pass `current_user` into GraphQL as context so you have access to user profile in the GraphQL resolver.

### Edges and Nodes Authorization

There are often multiple edges that lead to a particular node.

Defining permission on edges is not practical.

Put authorization logic into the **nodes** (type-level), such that they are enforced no matter how the node is reached in the graph.

## N+1 Problem

* It's easy to fall into N+1 problem in GraphQL.
* Using Ruby Fibre to solve N+1 problem innately? See Airbnb Graphist. Fibre will block until doing all aggregation.
* N+1 is a under-fetching problem

```
// 6 queries
// 1 query to find the rental
// and 5 queries to find the owners one by one
query {
  rentals {
    id
    owner {
      name
    }
  }
}
```

If we eager-load using Rails, then we are back to over-fetching issues. Instead, we need to use a batching approach like DataLoader or graphql-batch.

## Thinking in Graphs

Think in graphs, not endpoints.

* [Thinking in Graphs](http://graphql.org/learn/thinking-in-graphs/)
* **Hierarchical** - Most product development involves the creation and manipulation of view hierarchies. To achieve congruence with the structure of these applications, a GraphQL query itself is a hierarchical set of fields. The query is shaped just like the data it returns. It is natural way for product engineers to describe data requirements.
* Every query has the shape of a tree - i.e. **it is never circular**.

### Traversing Graphs

GraphQL makes traversing graphs (and therefore relational data) very easy. Based on the schema, you can retrieve data based on the relations they have.

This sample query let you:

1. Pull the name of users
2. Who've written reviews
3. On a business

Note that it is hierarchical.

```js
{
  business(id: "garaje-san-francisco") {
    reviews {
      user {
        name
      }
    }
  }
}
```

## Design Your Schema

> The schema is basically a capabilities document that has a list of all the questions which the client can ask the GraphQL layer.

Most languages have "classes" and "methods". Not GraphQL! As it has only "types" and "fields". But you can think of them as sort of the same:

```js
type User {
  name: String!
  friends: [User]!
  profilePicture: Image
}

class FBUser {
  public function getName(): string {
    return $this->name;
  }
}
```

Type have fields. Fields have types.

* [Break out the realm of URLs](https://dev-blog.apollodata.com/discourse-in-graphql-part-1-ee1ffd8a22df)

A Schema is just a collection of Types.

With SDL (Schema Definition Language). The schema tells the server what queries clients are allowed to make, and how different types are related.

A GraphQL schema defines types. Each type — except for scalar types like Int, Float or String — has fields which define the relationship between this type and other types (one to one, or one to many). If you think about your schema in terms of a graph, types are the nodes of your graph, and fields are edges. Scalar types have no fields, so they form the leaf nodes of your graph.

> A GraphQL query is just an instruction for traversing the graph in a specific way, resulting in a tree.

When traversing a tree, you would start at the root, but a graph has no root so there is no logical starting point! That's why every GraphQL schema needs to have a root query type: it's the entry point into the graph. The fields of the root query type are links to the actual queries that your GraphQL server supports.

```js
// It is common to have top-level query to be role-specific
type Query {
  me: User
  user(id: Int): User
}

type User {
  name: String
  profilePicture(size: Int = 50): ProfilePicture
  friends(first: Int, order_by: FriendOrderEnum): [User]
  events(first: Int): [Event]
}
```

Think about how you would traverse your graph, like for candidate:

```js
{
  // Single endpoint - useful as an entry point into your
  // object graph
  candidate(id: 123) {
    // List endpoint
    employments {
      period
      contracts {
        code
        leaves {
          day
        }
        timesheets {
          details {
            time_in
            time_out
          }
        }
      }
    }
  }
}
```

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

```js
const Page = new GraphQLObjectType({
  name: 'Page',
  description: 'Page of content',
  interfaces: [Collection],
  fields: {
    url: {
      type: GraphQLString,
      resolve: (it) => {
        return (it.sectionId ? `/stream/sectionsId/${it.sectionId}` : null)
      }
    },
    title: {
      type: GraphQLString
    },
    items: {
      type: new GraphQLList(Content),
      args: {
        from: { type: GraphQLInt },
        limit: { type: GraphQLInt },
        genres: { type: new GraphQLList(GraphQLString) }
      },
      resolve: (page, {from, limit, genres}, {backend}) => {
        return backend.contentv1(page.items, {from, limit, genres})
      }
    }
  }
})
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

## Field Naming

2 format for mutations:

* verbNoun - `createCustomer`
* nounVerb - `customerCreate` (Shopify's approach)

Shopify's approach is to name the noun first so it aid in advertising documentation, e.g. all the `customerXXX` will appear together.

## Object Type

Fields can return scalars like Int, String, Boolean.

Most of the fields you will be dealing with are List or Object.

Object types are fields that eventually resolve to scalar types or other objects/lists.

If there are no `resolve()` for a field, it will just be a method call to the parent object.

## Data Composition

* Query Composition - the parent component can gather up the child query and compose it into one single query request

The parent need to know the data requirement of the children and combine into one big query, so GraphQL need to be composable.

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

## Data Graph - Nodes and Edges

* Be careful of N+1 problem with many edges

## Type

Under-fetching is actually a type error.

## Fragments

> Fragment as a primitive - Fragment Models??

Fragments are the primary unit of composition in GraphQL. It allow for the reuse of common repeated selections of fields, reducing duplicated text in the document.

Fragments are a common unit of composition allowing for query reuse.

The composition of all GraphQL fragments equals the total data requirements of the app.

Fragments are consumed by using the spread operator (`...`).

```js
query {
  user(id: 4) {
    friends(first: 10) {
      ...friendFields
    }
  }
}

fragment friendFields on User {
  id
  name
  ...standardProfilePic
}

fragment standardProfilePic on User {
  profilePic(size: 50)
}
```

## Relay

**Declarative API** - Don't worry about HOW the data is fetched. Or even WHEN it is fetched. The framework orchestrates the data-fetching.

* Send queries/mutation without having to worry about lower-level networking details or maintaining a local cache
* Optimistic UI updates
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

```
yarn add react-relay
yarn add relay-compiler --dev
yarn add babel-plugin-relay --dev
```

## Relay Fragment Container



## Static Queries

## Data Loader

Please don't do REST API backing your GraphQL. It will be damn slow. Always use some variants of Data Loader.

* [graphql-batch for Ruby, sort of like DataLoader](https://github.com/Shopify/graphql-batch)
* [DataLoader - Source code walkthrough by Lee Byron](https://www.youtube.com/watch?v=OQTnXNCDywA)
* [Ruby BatchLoader](https://engineering.universe.com/batching-a-powerful-way-to-solve-n-1-queries-every-rubyist-should-know-24e20c6e7b94)
* [batch-loader](https://github.com/exAspArk/batch-loader)
* [dataloader](https://github.com/sheerun/dataloader)
* [graphql-query-resolver - Minimize N+1 queries](https://github.com/nettofarah/graphql-query-resolver)
* [Preloading Associations with graphql-batch](https://gist.github.com/mech/a2fb158c76f4617f72f0f8b6c48b80e1)

## Edges and Connections

Ability to traverse edges or connections, 1-to-many relationships.

* [Explaining GraphQL Connections - Edges have never been so fun!](https://dev-blog.apollodata.com/explaining-graphql-connections-c48b7c3d6976)
* [GraphQL Connections In Rails](http://graphqlme.com/2017/09/24/graphql-connections-rails/)

Connection is a collection of Edges

```js
type Company implements Node {
  id: ID!
  name: String
  industry: String
}

type CompaniesConnection {
  pageInfo: PageInfo!
  edges: [CompaniesEdge]
}

// Edge can be additional metadata properties like
// when the company was created, etc.
type CompaniesEdge {
  cursor: String!
  node: Company
}

// To query this connection
companiesConnection(first: 10) {
  edges {
    cursor
    node {
      id
      name
      industry
    }
  }
}
```

## Pagination

* [Understanding pagination: REST, GraphQL, and Relay](https://dev-blog.apollodata.com/understanding-pagination-rest-graphql-and-relay-b10f835549e7)
* [Twitter - Using cursors to navigate collections](https://dev.twitter.com/overview/api/cursoring)
* [GraphQ::Pro - Stable Cursors for ActiveRecord](http://graphql-ruby.org/pro/cursors)
* [Pagination: You're (Probably) Doing It Wrong](https://coderwall.com/p/lkcaag/pagination-you-re-probably-doing-it-wrong)
* [GraphQL Connections In Rails](http://graphqlme.com/2017/09/24/graphql-connections-rails/)
* [Slack API Pagination](https://api.slack.com/docs/pagination)
* [GraphQL Pagination Implementation](https://medium.com/@mattmazzola/graphql-pagination-implementation-8604f77fb254)

Instead of using literal page numbers, idiomatic GraphQL uses opaque strings called **cursors**. Cursors are more resilient to real-time changes to your data, which might lead to duplicates in simple page-based systems.

There are 2 pagination:

1. **Classic pagination** using `LIMIT` and `OFFSET/SKIP` - good for basic business-oriented resources like documents and users list.
2. **Cursor-based pagination** - for large list like Twitter/Facebook feed with Load More button. Not really situation for jumping to a specific page.

```
first = LIMIT the number of results
after = The next cursor value. An alternative to integer offset.
```

## Ruby - Parallelism

* [Issue 274 - First-class async support](https://github.com/rmosolgo/graphql-ruby/issues/274)
* ActionController::Live
* DeferredExecution

## Rails

`rails generate graphql:install --batch --no-graphiql --schema=ApiSchema`

* [**GraphQL and Performance in Rails**](https://blog.codeship.com/graphql-and-performance-in-rails/)
* [Building a full on GraphQL app](https://medium.com/ryancollinsio/building-a-full-on-graphql-app-b261f6cfea93)
* [How to Implement a GraphQL API in Rails](https://dzone.com/articles/how-to-implement-a-graphql-api-in-rails-via-codesh)
* [GraphQL + Relay Modern + Rails](https://collectiveidea.com/blog/archives/2017/08/03/graphql-relay-modern-rails)
* [Caching GraphQL queries with GraphQL-ruby and Rails](http://mgiroux.me/2016/graphql-query-caching-with-rails/)
* [graphql-ruby-demo](https://github.com/rmosolgo/graphql-ruby-demo)
* [File uploading with Rails + Apollo client](https://gist.github.com/github0013/d79fa651be3d7450adcd447676d01921)
* [graphql-preload](https://github.com/ConsultingMD/graphql-preload)
* [Presenter pattern for Rails and GraphQL](http://graphqlme.com/2017/09/30/presenterdecorator-pattern-in-graphql-rails/)
* [Caching GraphQL queries with GraphQL-ruby and Rails](http://mgiroux.me/2016/graphql-query-caching-with-rails/)
* [Using IDL instead of Ruby definition](https://github.com/rmosolgo/graphql-ruby/issues/727)
* [#820 - Object-oriented schema definition](https://github.com/rmosolgo/graphql-ruby/issues/820)

Raise `GraphQL::ExecutionError` if there are any errors.

`GraphQL::Introspection::INTROSPECTION_QUERY`

```ruby
class GraphqlController < ApplicationController
  def create
    result = Graph::Schema.execute(params[:query])
    render json: result
  end
end
```

```ruby
# type RootQuery {
#   restaurant(name: String): Restaurant
# }

module Graph::Types
  RootQuery = GraphQL::ObjectType.define do
    name 'RootQuery'
    
    field :restaurant do
      argument :name, types.String
      type Graph::Types::Restaurant
      
      resolve -> (object, arguments, context) do
        ::Restaurant.find_by(name: arguments['name'])
      end
    end
  end
end

# type Restaurant {
#   name: String
#   cuisine: String
# }

module Graph::Types
  Restaurant = GraphQL::ObjectType.define do
    name 'Restaurant'
    
    field :cuisine do
      type types.String
      
      resolve -> (restaurant, arguments, context) do
        restaurant.cuisine
      end
    end
  end
end
```

## Resolvers

* Resolve functions are like little routers.
* Each field in the query corresponds to a resolve() function
* ALL resolvers are called. Query is traversed field by field, executing "resolves" for each field.
* Complexity is pushed to the server-side resolvers where powerful machines can take care of the heavy computation work and caching
* [How is query executed?](https://dev-blog.apollodata.com/graphql-explained-5844742f195e)

Server developer can focus on **describing the data available** rather than implementing and optimizing specific endpoints.

The root query resolver will return a model for use on the next level of resolver and turtle all the way down.

There is a `resolve()` for every field, but this does not mean that an individual database query is required to fetch each field.

## Subscription

* [subscriptions-transport-ws](https://github.com/apollographql/subscriptions-transport-ws)
* [graphql-redis-subscriptions](https://github.com/davidyaha/graphql-redis-subscriptions)

## IDE Support

* [graphql-language-service](https://github.com/graphql/graphql-language-service)

## Introspection

```
▶ npm install -g get-graphql-schema

▶ get-graphql-schema -h 'Authorization=XXX' http://localhost:3000/graphql
```

## Tooling

https://www.youtube.com/watch?v=bQUYWYuVCP0

```
▶ yarn add graphql-cli
▶ graphql init
▶ graphql get-schema

eslint-plugin-graphql

.graphqlconfig

graphql/template-strings
graphql/named-operations
graphql/required-fields
```

* [graphql-docs by GitHub](https://github.com/gjtorikian/graphql-docs)
* [graphql-client](https://github.com/github/graphql-client)
* [apollo-fetch](https://github.com/apollographql/apollo-fetch)
* `brew cask install graphiql`
* [Expensive service - GraphQL::Pro](http://graphql.pro/)
* [graphql-cli](https://github.com/graphcool/graphql-cli)
* [apollo-codegen](https://github.com/apollographql/apollo-codegen)

Using `apollo-codegen` with queries and fragments. Attempting to use an undeclared field from a fragment declaration won't get caught by a linter, but will get caught by types.

```
curl -X POST \
"http://localhost:3000/graphql" \
-H "Content-Type: application/graphql" \
-H "Authorization: token" \
-d '
{
  me {
    name
  }
}
'
```

## Codegen

* [GraphQL Code-Generator 1.0](https://medium.com/@dotansimha/graphql-code-generator-a34e3785e6fb)

## Request Budgeting

* Maximum query time = 1 second?

## Caching

It turns out that the tree structure of GraphQL lends itself extremely well to client-side caching.

## Persisted Query

```
POST /graphql/eyBuawWNlIHsdfHj5IhoHJ0
```

## Examples

* [Yelp](https://www.yelp.com/developers/graphql/guides/intro)
* [Shopify](https://help.shopify.com/api/storefront-api/graphql)
* [MusicBrainz](https://github.com/exogen/graphbrainz/blob/master/docs/types.md)
* [northwind-graphql-ruby](https://github.com/tb/northwind-graphql-ruby)
* [Fullstack GraphQL](https://github.com/atulmy/fullstack-graphql)

## People

* [Marc-André Giroux](http://mgiroux.me/)
* [Robert Mosolgo](https://rmosolgo.github.io/blog/archives/)

## Videos

* [Lessons from 4 Years of GraphQL](https://www.youtube.com/watch?v=zVNrqo9XGOs)
* [High Performance GraphQL - DataLoader](https://www.youtube.com/watch?v=c35bj1AT3X8)
* [Using Apollo with ReactJS and GraphQL - SingaporeJS](https://www.youtube.com/watch?v=JCBVrE59yAI)
* [Optimizing for API Consumers with GraphQL](https://www.youtube.com/watch?v=psPnEUAL08w)
* [GraphQL at Facebook](https://www.youtube.com/watch?v=etax3aEe2dA)