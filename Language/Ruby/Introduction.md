# Ruby Introduction

* [Design Patterns in Ruby](https://github.com/davidgf/design-patterns-in-ruby)
* [Have Generics Killed Java?](http://www.artima.com/weblogs/viewpost.jsp?thread=299081)
* [11 Ruby Tricks You Haven't Seen Before](http://www.blackbytes.info/2016/01/ruby-tricks/)
* [Towards Minimal, Idiomatic, and Performant Ruby Code](https://blog.codeminer42.com/towards-minimal-idiomatic-and-performant-ruby-code-f3fc6aed3c94)
* [5 Ruby Methods You Should Be Using](https://www.engineyard.com/blog/five-ruby-methods-you-should-be-using)
* [Timeout: Ruby's Most Dangerous API](http://www.mikeperham.com/2015/05/08/timeout-rubys-most-dangerous-api/)
* [Ruby Users: Be Wary of Net::HTTP](https://engineering.wework.com/ruby-users-be-wary-of-net-http-f284747288b2)
* [The Ultimate Guide to Ruby Timeouts](https://github.com/ankane/the-ultimate-guide-to-ruby-timeouts)
* [Crafting Ruby](http://craftingruby.com/)

```ruby
# Singleton instance
Types::Post = GraphQL::ObjectType.define {
}

# Proc literals
# Slower than method calls
field :comments do
  argument :orderBy
  resolve ->(obj, args, ctx) {
    obj.comments.order(args[:orderBy])
  }
end
```

## Splat and Double Splat

* [Splat goes Ruby](https://dev.firmafon.dk/blog/splat-goes-ruby/)
* [Drat! - Ruby has a Double Splat](https://dev.firmafon.dk/blog/drat-ruby-has-a-double-splat/)

## Codemod

* [Refactoring Ruby programmatically](https://lethain.com/refactoring-programmatically/)
* [How to write a codemod](https://vramana.github.io/blog/2015/12/21/codemod-tutorial/)

## CSV

* [A Guide to the Ruby CSV Library - Part 2](https://www.sitepoint.com/guide-ruby-csv-library-part-2/)
* [Superfast CSV imports using PostgreSQL's COPY command](https://infinum.co/the-capsized-eight/superfast-csv-imports-using-postgresqls-copy)

## Ruby 2.5

* BigDecimal.new() is deprecated.

## Ruby 2.4

* [New Features in Ruby 2.4](https://blog.cognitohq.com/new-features-in-ruby-2-4/)

## Regular Expression

* [Onigmo](https://github.com/k-takata/Onigmo/blob/3ddfbfcc469a246f8c5bc50072c7e9cdb1e50b22/doc/RE#L293)

## Date and Time

* [UTC is enough for everyone, right?](https://zachholman.com/talk/utc-is-enough-for-everyone-right)
* [Timezone problem](https://www.youtube.com/watch?v=aUk9981C-fQ)
* [When should you use DateTime and when should you use Time?](https://gist.github.com/pixeltrix/e2298822dd89d854444b)
* [The Exhaustive Guide to Rails Time Zones](http://danilenko.org/2012/7/6/rails_timezones/)

```ruby
Date.parse(params[:start])
Date.iso8601(params[:start])

10.hours.from_now
7.days.ago

Time.zone.parse(string_containing_timestamp)

Time.strptime(
  "2017-08-27T12:09:36Z",
  "%Y-%m-%dT%H:%M:%S%z"
).in_time_zone

Time.current
Time.current.utc.iso8601

a_time_instance.in_time_zone

Date.current # take into account timezone
Date.today   # don't use this, not timezone-aware

# Avoid these
Time.now
Date.today
Time.parse() # Very problematic as it will fallback to Time.now when any part of the string could not be parsed
Time.strptime()
```

* Do not store dates as `DateTime`
* Be very careful of `DateTime` to `Date` conversion
* Be very careful of `Date` to `DateTime` conversion

## Integer

```ruby
# if params return nil, the result will be 0, may or may not be serious error
params[:id].to_i

# More stricter form of getting ID
Integer(params.fetch(:id))
```

## Delegation

* [The Gang of Four is wrong and you don't understand delegation](https://www.saturnflyer.com/blog/the-gang-of-four-is-wrong-and-you-dont-understand-delegation)

## Enumerable

* [Five Ruby methods your should be using](https://blog.engineyard.com/2015/five-ruby-methods-you-should-be-using)
* [101 Ruby Code Factoids](https://6ftdan.com/allyourdev/2016/01/13/101-ruby-code-factoids/)
* [The === (case equality) operator in Ruby](http://blog.arkency.com/the-equals-equals-equals-case-equality-operator-in-ruby/)

```ruby
array = [1, 2, 3, 4, 5]
first, *rest = array
puts first # => 1
puts rest  # => [2, 3, 4, 5]
```

### inject/reduce - Ruby's fold

```ruby
# Not memory efficient
# You need to gather all the keys and then do a final flatten
def keys(hashes)
  hashes.map(&:keys).flatten.uniq
end

# Pass a Set to inject
# Our default is an empty Set and we do a set union on the key
def keys(hashes)
  hashes.inject(Set.new) { |accumulator, hash|
    accumulator | hash.keys
  }.to_a
end
```

### flat_map

```ruby
users.map do |user|
  user.posts.map do |post|
    post.comments.map |comment|
      comment.author.username
    end
  end
end

# => [[['Ben', 'Sam', 'David'], ['Keith']], [[], [nil]]]
```

This gives us a lot of unwanted nested arrays, we can use `flatten`.

```ruby
users.map do |user|
  user.posts.map do |post|
    post.comments.map |comment|
      comment.author.username
    end.flatten
  end.flatten
end.flatten
```

Or we can use `flat_map` also.

```ruby
users.flat_map do |user|
  user.posts.flat_map do |post|
    post.comments.flat_map |comment|
      comment.author.username
    end
  end
end
```


## instance_eval

```ruby
app = Rack::Builder.new do
  use Rack::Cache, verbose: true
  use Rack::Static, root: 'public'
  run Rack::Lobster.new
end

class Rack::Builder
  def initialize(&block)
    @use = []
    instance_eval(&block)
  end
  
  def use(middleware, *args)
    @use << lambda { |app| middleware.new(app, *args) }
  end
  
  def run(app)
    @app = @use.reverse.inject(app) do |chain, use|
      use.call(chain)
    end
  end
  
  def call(env)
    @app.call(env)
  end
end
```

## Double Splat Operator

```ruby
def start(**attributes)
  defaults = { uuid: SR.uuid }
  cmd = NewSession.new(defaults.merge(attributes))
  command.call(cmd)
end
```

## yield_self

* [As compared to Elixir's pipe operator](https://robots.thoughtbot.com/using-yieldself-for-composable-activerecord-relations)

## Frozen String

* [Freeze string literals when not mutated](https://github.com/rails/rails/pull/20946)
* [let_it_go](https://github.com/schneems/let_it_go)

Affected behaviors:

```ruby
# String interpolation
.gsub!
.downcase!
<<

name.dup # Make an unfrozen copy of the string and do your modification
```

## Problem Solving

* [Pair with Sum](http://routetomastery.com/blog/2017/01/08/has-pair-with-some-problem/)

## People & Blog

* [Aaron Lasseigne](https://aaronlasseigne.com/)
* [Shopify Engineering Blog](https://engineering.shopify.com/blogs/engineering)
* [Appfolio](http://engineering.appfolio.com/)
* [Infinum](https://infinum.co/the-capsized-eight)

## Videos

* [Drifting Ruby](https://www.driftingruby.com/episodes)
* [Therapeutic Refactoring by Katrina Owen](https://www.youtube.com/watch?v=J4dlF0kcThQ)
* [Refactoring from Good to Great by Ben Orenstein](https://www.youtube.com/watch?v=DC-pQPq0acs)
* [Type. Context. by Sam Phippen](https://www.youtube.com/watch?v=qzTOnnDePtc)
* [Nothing is Something - Sandi Metz](https://www.youtube.com/results?search_query=nothing+is+something+sandi+metz)

## Books

* Domain-Driven Rails - Page 76/187

