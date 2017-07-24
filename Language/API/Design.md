# API Design

APIs should be a key component of your deployment strategy. Without a widespread deployment of APIs, you can forget about deploying your final product in a timely fashion and within your budget.

* [Test HTTP status code](http://httpstat.us/)
* [Rails 5 API Tutorial](https://github.com/vasilakisfil/rails5_api_tutorial)
* [active_hash_relation](https://github.com/kollegorna/active_hash_relation)
* [REST without PUT](https://www.thoughtworks.com/radar/techniques/rest-without-put)
* [Best Practices for Designing a Pragmatic RESTful API](http://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api)
* [How and why should you use JSON API in your Rails API?](http://blog.arkency.com/2016/02/how-and-why-should-you-use-json-api-in-your-rails-api/)
* [Writing a Hypermedia API client in Ruby](https://robots.thoughtbot.com/writing-a-hypermedia-api-client-in-ruby)
* [Designing robust and predictable APIs with idempotency](https://stripe.com/blog/idempotency)
* [REST Anti-Patterns](https://www.infoq.com/articles/rest-anti-patterns)
* [Ultimate Guide to API Design](https://blog.qmo.io/ultimate-guide-to-api-design/)

---

* Resource URI
* Resource Representation
* API Operations (Verbs)

Don't confuse domain entities in DDD with resources in REST API. Business processes/operations can also be a resource.

* Noun Resource - e.g. Account. Identifiable, queryable for current state. Stateful.
* Verb Resource - e.g. ChangeOfAddress. Immutable, treat it like an event, fire and forget, no tracking of state, stateless

Focus on business capabilities.

```ruby
class CustomersController < ApplicationController
  def enroll
  end
end

# Instead of using the Customer resource, we are using a
# resource which is the equivalent of a request to enroll
# customer
class CustomerEnrollmentsController < ApplicationController
  def create
  end
end

# Be more RESTful
class DiscountsController < ApplicationController
  def create
  end
end

Rails.application.routes.draw do
  resource :cart do
    resource :discount, only: :create, controller: :cart_discounts
  end
end

# Instead of this which is not really RESTful
class CartsController < ApplicationController
  def apply_coupon
  end
end

Rails.application.routes.draw do
  resource :cart do
    get :apply_coupon
  end
end
```

> GitHub API is a good example of a reasonably well designed API in the public domain with right resource granularity. For example, creating a fork is an asynchronous operation. GitHub supports the reified "Forks" sub-collection resource that can be used to list existing forks or create a new fork. Performing code "merge" using merges sub-collection resource is another example of reification of the "merge" concept and the underlying merge operation. On the other hand, GitHub also supports many low level resources such as Tag. Most of the real world APIs will require both coarse grained aggregate resources and also low level "nouns in the domain" resources. - [REST API Design Resource Modeling](https://www.thoughtworks.com/insights/blog/rest-api-design-resource-modeling)

```
// How to deal with actions that fit CRUD
// Star and un-star a gist at GitHub

PUT /gists/:id/star
DELETE /gists/:id/star
```

## Versioning

* [Versioning a Rails API](https://chriskottom.com/blog/2017/04/versioning-a-rails-api/)
* [Your API versioning is wrong, which is why I decided to do it 3 different wrong ways](https://www.troyhunt.com/your-api-versioning-is-wrong-which-is/)

## Analytics

Track your API/endpoints call by incrementing counters. The most commonly used API calls should be made efficient.

## Methods

* [POST != Create and PUT != Update](http://www.eq8.eu/blogs/37-post-create-and-put-update)

## JSON Schema

## JSONAPI

* [JSON API Format](http://jsonapi.org/format/)
* [Lots of client/server implementations](http://jsonapi.org/implementations/)
* [jsonapi-resources](https://github.com/cerebris/jsonapi-resources)
* [jsonapi-utils](https://github.com/tiagopog/jsonapi-utils)
* [jsonapi-serializers](https://github.com/fotinakis/jsonapi-serializers)
* [Rails JSON API Tutorial - Using JSONAPI Resources gem](http://tutorialsfordevs.com/tutorials/rails-json-api-tutorial/)

## OpenAPI

## Sparse Fields

```
?fields=id,subject,name,updated_at
```

## Sorting and Pagination

People either use link header or envelope like `meta`.

* [Link header introduced by RFC 5988](https://tools.ietf.org/html/rfc5988#page-6)

```
?filter[title]=

// Sort rating in desc order and if there is a tie, use title to break them up
?sort=-rating,title

// Retrieves a list of tickets in descending order of priority
GET /tickets?sort=-priority

// Retrieves recently updated tickets
GET /tickets?sort=-updated_at

// Retrieve the highest priority open tickets mentioning the word 'critical'
GET /tickets?q=critical&state=open&sort=-priority,created_at
```

```
meta: {
  page-count: 3,
  record-count: 27
}
```

## Filtering Collections

* [filterable](https://github.com/procore/filterable)

## Form Input

Do not use URL encoding when submitting form. Rather use JSON as submission body.

URL encoding has no concept of data types. This forces the API to parse integers and booleans out of strings. It also has no concept of hierarchical structure, you have to append `[]` to represent array for example.

When you submit JSON input, be sure to set Content-Type header also or throw **415 Unsupported Media Type** error.

## Rate Limiting

Return **429 Too Many Requests**

```
X-Rate-Limit-Limit
X-Rate-Limit-Remaining
X-Rate-Limit-Reset

// GitHub example
X-GitHub-Media-Type: github.v3; format=json
X-GitHub-Request-Id: DF5A:08A1:25571A7:30178E3:58FF0E5A
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
X-RateLimit-Reset: 1493113962
X-Served-By: a30e6f9aa7cf5731b87dfb3b9992202d
```

## Examples

* [Stripe API](https://stripe.com/docs/api)
* [StackExchange](https://api.stackexchange.com/docs/compression)
* [GitHub v3](https://developer.github.com/v3/)
* [GitHub GraphQL](https://developer.github.com/early-access/graphql/)
* [Enchant](http://dev.enchant.com/api/v1)

## Videos

* [Rails APIs: The Next Generation](https://www.youtube.com/watch?v=iTbTz8_ztIM)