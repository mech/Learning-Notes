# Ruby Introduction

* [Design Patterns in Ruby](https://github.com/davidgf/design-patterns-in-ruby)
* [Have Generics Killed Java?](http://www.artima.com/weblogs/viewpost.jsp?thread=299081)
* [11 Ruby Tricks You Haven't Seen Before](http://www.blackbytes.info/2016/01/ruby-tricks/)

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

## People

* [Aaron Lasseigne](https://aaronlasseigne.com/)
