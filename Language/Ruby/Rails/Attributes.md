# Attributes

* [dry-types](https://dry-rb.org/gems/dry-types/)
* [Stripe's type implementation for Ruby](https://sorbet.run/)
* [attributes.rb](https://github.com/rails/rails/blob/master/activerecord/lib/active_record/attributes.rb)
* [store_configurable](https://github.com/metaskills/store_configurable)

ActiveRecord's types have been moved to ActiveModel and each needs their own `serialize(value)` implementation vs the old `type_cast_for_database(value)`.

# Validation

* [Custom type-casting with ActiveRecord, Virtus and dry-types](http://blog.arkency.com/2016/03/custom-typecasting-with-activerecord-virtus-and-dry-types/)
* [dry-validation](http://dry-rb.org/gems/dry-validation/)
* [Always use the new "Sexy Validation" introduced in Rails 3](http://thelucid.com/2010/01/08/sexy-validation-in-edge-rails-rails-3/)
* [Validation, Database Constraint, or Both?](https://robots.thoughtbot.com/validation-database-constraint-or-both)

```ruby
class RecurringEvent < ApplicationRecord
  TIME_12H_FORMAT = /\A(1[0-2]|0?[1-9]):[0-5][0-9]\s?(am|pm)\z/i
  validates :time, presence: true, format: { with: TIME_12H_FORMAT, message: 'invalid time - use format 10:00 am' }
end
```

## Attributes API

Starting from Rails 5, ActiveModel will get Attributes module also.

```ruby
class Customer
  include ActiveModel::Attributes
  
  attribute :name, :string
  attribute :age, :integer
end
```

* [Introduction to ActiveRecord and ActiveModel Attributes API](https://karolgalanciak.com/blog/2016/12/04/introduction-to-activerecord-and-activemodel-attributes-api/)