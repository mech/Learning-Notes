# Exceptions and Errors

> `begin` keyword is a code smell in Ruby. It is nothing wrong, just a warning sign.

* [Exceptional Ruby - Avdi](http://avdi.org/talks/exceptional-ruby-rubyconf-2011/exceptional-ruby.html)
* [Rescuing Exceptions in Ruby: A Primer](http://blog.appsignal.com/blog/2016/10/18/ruby-magic-exceptions-primer.html)
* [Airbrake's Ruby Exception Handling series](https://airbrake.io/blog/category/ruby-exception-handling)
* [How to control an application flow?
](https://blog.lelonek.me/how-to-control-application-flow-e97895a60b3c#.yobp7071i)

```ruby
# Make warning be error only with -d flag
if $DEBUG
  module Kernel
    def warn(message)
      raise message
    end
  end
end
```

It's tempting to raise an exception every time you get an answer you don't like. But exception handling interrupts and obscures the flow of your business logic. Consider carefully whether a situation is truly unusual before raising an Exception.

Exception should only be used for unexpected situations. Use `throw` for expected cases.

## Performance

There is no penalty simply for having exception handling code lying around dormant.

On the other hand, writing code that uses exceptions as part of its logic can have a significant performance cost.

## StandardError

`StandardError` encompasses all normal, expected exceptions that your application may encounter during execution. They can all be dealt with without any detrimental effects because they are "expected".

Conversely, exceptions outside of the scope of `StandardError`, which simply fall elsewhere under the superclass of `Exception` are inherently system-level errors, and thus will typically indicate a non-functional application.

* [Exceptions should not be expected!](https://robots.thoughtbot.com/save-bang-your-head-active-record-will-drive-you-mad)

## Caller-Supplied Fallback

```ruby
def render_user(user)
  if user.fname && user.lname
    "#{user.lname}, #{user.fname}"
  else
    yield
  end
end

# Fall back to a benign placeholder value
render_user(user) { 'UNKNOWN USER' }
```

## Libraries

* [StackExchange.Exceptional](https://github.com/NickCraver/StackExchange.Exceptional)