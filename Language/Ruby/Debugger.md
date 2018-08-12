# Debugger

* [I am a puts debuggerer](https://tenderlovemaking.com/2016/02/05/i-am-a-puts-debuggerer.html)
* [nrdebug.rb](https://github.com/newrelic/rpm/blob/master/bin/nrdebug)
* [Linux Perf](http://www.brendangregg.com/linuxperf.html)

```ruby
bundle exec gem pristine <any_gem_you_modified>

def method_code_i_want_to_debug
  require 'irb'; binding.irb
end

caller.grep(Regexp.new(Regexp.quote(__dir__)))
```

```
// Ignore white space changes
git blame -w
```

## Introspection

```ruby
# Use this to fill in knowledge gap between API doc and real source
Post.method(:create).source_location
```

## Trace Point

## Videos

* [Practical Debugging](https://www.youtube.com/watch?v=oi4h30chCz8)
* [Perusing the Rails Source Code](https://www.youtube.com/watch?v=Q_MpGRfnY5s)

