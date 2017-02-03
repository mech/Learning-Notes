# Attributes

* [attributes.rb](https://github.com/rails/rails/blob/master/activerecord/lib/active_record/attributes.rb)
* [store_configurable](https://github.com/metaskills/store_configurable)

ActiveRecord's types have been moved to ActiveModel and each needs their own `serialize(value)` implementation vs the old `type_cast_for_database(value)`.