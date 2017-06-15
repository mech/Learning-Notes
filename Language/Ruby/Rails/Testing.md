# Rails Testing

* [How to Write Better Code Using Mutation Testing](https://blog.cognitohq.com/how-to-write-better-code-using-mutation-testing/)

## Integration Tests

> In my experience, I've learned that the codebase with good unit test coverage is generally more error-prone than the one with good integration test coverage. I noticed that the majority of bugs introduced with developing work are regression bugs. An unit tests are usually not very good in catching those.

## Fixtures

* [Testing a Rails API](https://johnmosesman.com/post/testing-a-rails-api/)

When Rails boots up the testing environment, it reads all the fixture definitions and insert them directly into the database, indiscriminately, bypassing validations and callbacks.

Your test data starts to form a narrative. A story takes shape around your models.

* [Getting friendly with fixtures](https://whatdoitest.com/getting-friendly-with-fixtures)
* [7 reasons I'm sticking with Minitest and Fixtures in Rails](http://brandonhilkert.com/blog/7-reasons-why-im-sticking-with-minitest-and-fixtures-in-rails/)
* [Rails Testing Antipatterns: Fixtures and Factories](https://semaphoreci.com/blog/2014/01/14/rails-testing-antipatterns-fixtures-and-factories.html)

## Controller Tests

* [Changes to test controllers in Rails 5](http://blog.bigbinary.com/2016/04/19/changes-to-test-controllers-in-rails-5.html)

Integration tests can serve as a replacement for controller tests. Integration tests are used to test the most important workflows of applications, while unit tests make sure individual parts work.

## Minitest

```ruby
assert_includes ANSWERS, ask('whatever')
assert_kind_of Array, ANSWERS
refute_empty ANSWERS

assert_raises 'Some error' do
end
```