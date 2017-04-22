# API Design

APIs should be a key component of your deployment strategy. Without a widespread deployment of APIs, you can forget about deploying your final product in a timely fashion and within your budget.

* [Test HTTP status code](http://httpstat.us/)
* [Rails 5 API Tutorial](https://github.com/vasilakisfil/rails5_api_tutorial)
* [active_hash_relation](https://github.com/kollegorna/active_hash_relation)

## Versioning

* [Versioning a Rails API](https://chriskottom.com/blog/2017/04/versioning-a-rails-api/)
* [Your API versioning is wrong, which is why I decided to do it 3 different wrong ways](https://www.troyhunt.com/your-api-versioning-is-wrong-which-is/)

## Methods

* [POST != Create and PUT != Update](http://www.eq8.eu/blogs/37-post-create-and-put-update)

## JSON Schema

## JSONAPI

* [JSON API Format](http://jsonapi.org/format/)

## OpenAPI

## Sparse Fields

## Sorting and Pagination

```
?filter[title]=

// Sort rating in desc order and if there is a tie, use title to break them up
?sort=-rating,title
```

```
meta: {
  page-count: 3,
  record-count: 27
}
```

## Filtering Collections