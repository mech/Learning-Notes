# Ruby Introduction

* [Design Patterns in Ruby](https://github.com/davidgf/design-patterns-in-ruby)
* [Have Generics Killed Java?](http://www.artima.com/weblogs/viewpost.jsp?thread=299081)
* [11 Ruby Tricks You Haven't Seen Before](http://www.blackbytes.info/2016/01/ruby-tricks/)

## Ruby 2.4

* [New Features in Ruby 2.4](https://blog.cognitohq.com/new-features-in-ruby-2-4/)

## Date

* [Timezone problem](https://www.youtube.com/watch?v=aUk9981C-fQ)

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
Time.parse()
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

## Frozen String

* [Freeze string literals when not mutated](https://github.com/rails/rails/pull/20946)
* [let_it_go](https://github.com/schneems/let_it_go)

## Problem Solving

* [Pair with Sum](http://routetomastery.com/blog/2017/01/08/has-pair-with-some-problem/)

## People & Blog

* [Aaron Lasseigne](https://aaronlasseigne.com/)
* [Shopify Engineering Blog](https://engineering.shopify.com/blogs/engineering)

## Videos

* [Drifting Ruby](https://www.driftingruby.com/episodes)