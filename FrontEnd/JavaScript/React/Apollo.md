# Apollo Client

* [apollo-tracing](https://github.com/apollographql/apollo-tracing)

```js
const logger = (operation, forward) => {
  const { operationName, query, variables, context } = operation
  
  console.group(operationName)
  console.log({ operationName, variables, query: print(query) })
  
  // make request
  return forward(operation).map(({ data, errors }) => {
    console.log({ data, errors })
    console.groupEnd()
    return { data, errors }
  })
}

const client = new ApolloClient({
  cache: new InmemoryCache(window.__APOLLO_STATE__),
  link: new ApolloLink.from([logger, link])
})

<ApolloProvider client={client}>
  <Router>
    <App />
  </Router>
</ApolloProvider>
```

### 2.0 Migration

* [Real official 2.0 migration guide](https://www.apollographql.com/docs/react/2.0-migration.html)
* [Some 2.0 migration guide](https://github.com/apollographql/apollo-client/blob/master/docs/source/2.0-migration.md)

## Apollo Link

> Creating a component-based request chain. Apollo Link is a request primitive designed for the GraphQL age.

One of the most important features of Apollo Client 2.0 is the move to a network layer powered by observables, instead of promises.

You can compose links to create complex control flows of GraphQL request.

* [Evans Hauser - one of Apollo Link author](https://medium.com/@evanshauser)
* [Creating a data component with Apollo Link](https://dev-blog.apollodata.com/creating-a-data-component-with-apollo-link-f0719d8193ee)
* [Apollo Link: Creating your custom GraphQL client](https://dev-blog.apollodata.com/apollo-link-creating-your-custom-graphql-client-c865be0ce059)

---

* RetryLink
* HttpLink
* apollo-link-offline - Collect operations while user has no network connection and replay them when the app comes back online.
* Terminating link is the one that doesn't use forward, but instead turns the operation into the result directly. Typically the final network request.

```js
import {
  ApolloLink,
  HttpLink,
  RetryLink
} from 'apollo-link'

const link = ApolloLink.from([
  new RetryLink(),
  new HttpLink({ uri })
])
```

Possibilities of Apollo Link:

* Request de-duplication
* Custom directives
* Offline support
* Retrying requests
* Pluggable caching
* Partial operation completion
* Persisted queries
* Single request to multiple locations

## Apollo Cache

* InmemoryCache
* [apollo-cache-hermes](https://github.com/convoyinc/apollo-cache-hermes)

## Query

```js
// Execute query and make this.props.data available
export default graphql(gql`
  query allPosts {
    posts {
      id
      title
    }
  }
`)(PostList)
```

## update() vs refetchQueries()

* Recommend to use update() for optimistic UI update

## Mutation

```js
takeLeaves = async() => {
  const { serviceCode, workMonth } = this.state
  
  await this.props.takeLeavesMutation({
    variables: {
      serviceCode,
      workMonth
    }
  })
  
  // Since it is async/await, we can write in normal flow
  this.props.history.push('/leaves')
}
```

* [Imperative store API](https://dev-blog.apollodata.com/apollo-clients-new-imperative-store-api-6cb69318a1e3)

```js
// the props option is how <NewPage> will get
// this.props.submit(body)
// mutate() return a promise and is the function provided by
// Apollo for you to perform mutation operation
graphql(mutation, {
  props: ({ mutate }) => ({
    submit: body => mutate({ variables: { body } }).catch()
  })
})(NewPage)

// Using compose
import { compose, gql, graphql } from 'react-apollo'

compose(
  withRouter,
  graphql(mutation, {
    // You can rename the mutate() function to a better name
    name: 'createPage',
    props: ({ createPage, ownProps: { history } }) => ({
      submit: body => createPage({ variables: { body } }),
      redirect: () => history.push('/')
    })
  })
)(NewPage)
```


## react-apollo

```js
const MovieQuery = gql`
  query Movie($id: Int!) {
    movie(id: $id) {
      title
      poster
    }
  }
`

export default graphql(MovieQuery, {
  props: ({ data }) => {
    if (!data.movie) {
      return { loading: data.loading }
    }
    
    return {
      loading: data.loading,
      movie: data.movie
    }
  },
  options: ({ id }) => ({ variables: { id } })
})(MovieCard)
```

## Fragments

```js
import { userFragment } from './fragments'

export const App = ({ data: { loading, currentUser } }) => {
}

const query = gql`
${userFragment}

query appQuery {
  currentUser: User {
    ...UserFields
  }
}

export default graphql(query)(App)
`
```

```js
// in fragments.js
import { gql } from 'react-apollo'

export const userFragment = gql`
fragment UserFields on User {
  id
  username
  full_name
  avatar_url
}
`
```

## Queries Merging

* [See queries merging section](https://marmelab.com/blog/2017/09/07/dive-into-graphql-part-iv-building-a-graphql-client-with-reactjs.html)

## Subscription

* [Introducing GraphQL Subscriptions - Lee Byron](https://www.youtube.com/watch?v=bn8qsi8jVew)

## @defer

## @rest

