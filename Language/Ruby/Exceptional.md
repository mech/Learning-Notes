# Exceptions and Errors

> Don't rescue just because you can. It's ok to crash in rare or unknown circumstances.

---

> `begin` keyword is a code smell in Ruby. It is nothing wrong, just a warning sign.

* [Exceptional Ruby - Avdi](http://avdi.org/talks/exceptional-ruby-rubyconf-2011/exceptional-ruby.html)
* [Rescuing Exceptions in Ruby: A Primer](http://blog.appsignal.com/blog/2016/10/18/ruby-magic-exceptions-primer.html)
* [Airbrake's Ruby Exception Handling series](https://airbrake.io/blog/category/ruby-exception-handling)
* [How to control an application flow?](https://blog.lelonek.me/how-to-control-application-flow-e97895a60b3c#.yobp7071i)
* [Advanced Rescue & Raise](http://docs.honeybadger.io/ruby/exceptions/advanced-rescue-and-raise.html)

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

```ruby
begin
rescue => e
end

# Is equivalent to
begin
rescue StandardError => e
end

# Default for raise is RuntimeError
# Default for rescue is StandardError

# Since RuntimeError is a subclass of StandardError, when you rescue
# with no specific, it will also catch RuntimeError.
class RuntimeError < StandardError
end

# Never do this since Exception is the root of the error hierarchy
# you will catch other system error thing like
# SystemStackError, NoMemoryError, SignalException, etc
begin
rescue Exception => e
end
```

```ruby
# Adding severity and metadata is good for filtering
begin
rescue => e
  Procore::ErrorHandler.handle(e, severity: :warn, metadata: {
    tool: :onboarding
  })
end
```

## Error Hierarchy

```ruby
Store::Error
Store::PurchaseError
Store::InventoryError
Store::CouponError
Store::OutOfSeasonError
Store::SecurityError
Store::PermissionError
Store::ReadOnlyError

# Different error need to go to different path
def create
rescue InventoryError => ie
  Store::Handler.handle(ie, { user_id: @user.id }, :warn)
  redirect_to shopping_cart_path
rescue CouponError => ce
  Store::Handler.handle(ce, { user_id: @user.id }, :info)
  redirect_to apply_coupon_path
end

class Store::Error < StandardError
  attr_accessor :metadata
  attr_accessor :severity
  
  def initialize(message, metadata = {}, severity = :error)
    super(message)
    @metadata = metadata
    @severity = severity
  end
  
  def user_message
    I18n.t('errors.unknown')
  end
end

# Empty class, but still useful
class Store::PurchaseError < Store::Error
end
```

## Rescue and Re-Raise

Great for control flow.

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

## Learn from Go

```ruby
require 'faraday'

# Machine communication scales better than human communication
# Go does forced error handling very way
# Ruby is a happy path obsessed ecosystem, so sometimes we need to force it
def get(url, on_success:, on_failure:)
  f = Faraday.new { |c| c.adapter Faraday.default_adapter }
  
  begin
    resp = f.get(url)
    on_success.call(resp)
  rescue Faraday::ClientError => e
    on_failure.call(e)
  end
end
```

## Libraries

* [StackExchange.Exceptional](https://github.com/NickCraver/StackExchange.Exceptional)
* [rusen](https://github.com/moove-it/rusen)

## Videos

* [The Arcane Art of Error Handling by Brad Urani](https://www.youtube.com/watch?v=9R4wlyWBP1k)