# Models

* [**Rails Database Practices**](http://blog.carbonfive.com/2016/11/16/rails-database-best-practices/)
* [7 Design Patterns to Refactor MVC Components in Rails](https://www.sitepoint.com/7-design-patterns-to-refactor-mvc-components-in-rails/)
* [7 Patterns to Refactor Fat ActiveRecord Models](http://blog.codeclimate.com/blog/2012/10/17/7-ways-to-decompose-fat-activerecord-models/)
* [Gourmet Service Objects](http://brewhouse.io/blog/2014/04/30/gourmet-service-objects.html)
* [Service objects in Rails will help you design clean and maintainable code. Here's how.](https://www.netguru.co/blog/service-objects-in-rails-will-help)
* [The World Needs Another Post About Dependency Injection in Ruby](http://solnic.eu/2013/12/17/the-world-needs-another-post-about-dependency-injection-in-ruby.html)
* [Testing Network Services in Ruby Is Easier Than You Think](http://www.justinweiss.com/articles/testing-network-services-in-ruby//)
* [Composition by James Dabbs](https://www.youtube.com/watch?v=zwo7ZTHS8Wg)
* [Getting Rails on Track - Part 3: Controllers](https://8thlight.com/blog/christoph-gockel/2016/11/02/getting-rails-on-track-part-3-controllers.html)
* [Build Sleek Rails Components With Plain Old Ruby Objects](https://www.toptal.com/ruby-on-rails/decoupling-rails-components)
* [Improving Large Rails Apps with Service Objects](https://aaronlasseigne.com/2016/04/27/improving-large-rails-apps-with-service-objects/)
* [Chain service objects](https://medium.com/@apneadiving/chain-service-objects-like-a-boss-35d0b83606ab#.9yci8ds4z)
* [My Rails Models Are Bloated. Should I Use Concerns?](http://www.rubypigeon.com/posts/rails-models-bloated-should-i-use-concerns/)
* [Good Module, Bad Module](https://blog.codeship.com/good-module-bad-module/)
* [Ruby Blog Pro](http://rubyblog.pro/)
* [Flag argument is a code smell](http://craftingruby.com/posts/2017/05/04/flag-arguments-are-a-code-smell.html)
* [Using Services to Keep Your Rails Controllers Clean and DRY](https://blog.engineyard.com/2014/keeping-your-rails-controllers-dry-with-services)

## Builder Patterns

* [Builder design pattern in Ruby](https://medium.com/kkempin/builder-design-pattern-in-ruby-dfa2d557ff1b)

```rb
CandidateBuilder.build do |builder|
  builder.set_name('mech')
  builder.is_admin
end

class CandidateBuilder
  def self.build
    builder = new
    yield builder
    builder.user
  end
  
  def initialize
    @user = Candidate.new
  end
  
  def set_name(name)
    @user.name = name
  end
  
  def is_admin
    @user.roles = ['admin']
  end
  
  def user
    @user
  end
end
```

## SQL

```ruby

```

## Query

* [To join or not to join? An act of #includes](https://goiabada.blog/to-join-or-not-to-join-an-act-of-includes-f6728fcefea3)
* [Active Record's queries tricks](https://medium.com/@apneadiving/active-records-queries-tricks-2546181a98dd)

```ruby
# Bad
Post.select(:id).map(&:id)

# Good
Post.pluck(:id)

# User model
scope :activated, -> {
  joins(:profile).where(profiles: { activated: true })
}

# Instead of leaking profile logic inside User model, we can:

# Profile model
scope :activated, -> { where(activated: true) }
# User model
scope :activated, -> { joins(:profile).merge(Profile.activated) }
```

## Database

* [Database constraints made easy for ActiveRecord](https://github.com/nullobject/rein)
* [Validation, Database Constraint, or Both?](https://robots.thoughtbot.com/validation-database-constraint-or-both)
* [Database views for Rails](https://github.com/thoughtbot/scenic)
* [How to Check if a Record Exists](https://semaphoreci.com/blog/2017/03/14/faster-rails-how-to-check-if-a-record-exists.html)
* [Compare password using BCrypt in Postgres](https://gist.github.com/Jacob-Kroeze/e0fa429e2b273f93ad65)

Each uniqueness constraint must be backed by a unique database index to protect against race conditions.

## Validation

* [Custom Validators in Ruby on Rails 4](http://www.rails-dev.com/custom-validators-in-ruby-on-rails-4)
* [Data Corruption: Stop the Evil Tribbles](https://www.youtube.com/watch?v=kA8aR1ffoOg)

---

1. Service Object
2. Form Object
3. Value object
4. Query Object
5. View Object
6. Policy Object
7. Decorator

```ruby
class Unit < ActiveRecord::Base
  validates :tracking_barcode, presence: true
  
  with_options on: :shipment_to_vendor do
    validates :product_id, presence: true
    validates :vendor_id, presence: true
  end
end

# custom validation contexts
@unit.save!(context: :shipment_to_vendor)

# Service object
UnitShippedToVendor.new(@unit).save!
```

```ruby
# Using Dry Validation
class MyFormObject
  self.schema = Dry::Validation.Form do
    optional(:attributes).maybe(:hash?)
    optional(:remember_me).maybe(:bool?)
    optional(:email).maybe(:str?)
    optional(:note).maybe(:str?)
  end
end
```

## Service Object

> Service layers are all about verbs.

* Specific to a use-case.
* Can also be seen as a Command Object, to use a design pattern name for it.
* Define application boundary that establishes a set of available operations.
* Encapsulate cross-cutting operations. Involves several models.
* Encapsulate a single process of the business logic. Describe one business rule only.
* Is functional, don't store any states. Services get input and produce output.

In Rails, controller is the boundary we want to separate. Service Object is the bridge between controller boundary and domain object. Controller's `params` acts as input and Service Object's output determine result (`render` or `redirect`).

```ruby
def create
  form = TimesheetService::Form.new(params)
  
  # Form object can quickly bailout if it is not even valid
  if form.valid?
    result = TimesheetService::Save.new(form)
    # result = TimesheetService.save(self)
    
    # Result is the next deeper level of bailout when
    # contract with third-party service
    result.success? ? render_ok(result) : render_error(result)
  else
    render_error(form)
  end
rescue ServiceError => e
  Audit::Exceptional.error(e)
end
```

Most Services use the `call()` so you can use a closure as well. Some services also use `execute()`.

Some services use verbs instead of nouns: `Movies::Create` vs `Movies::Creator`.

## Form Object

* [Decouple Your Models with Form Objects](https://www.youtube.com/watch?v=d9vMENoqxEE)
* [18 Con-Struct Attributes Gems](http://idiosyncratic-ruby.com/18-con-struct-attributes.html)
* [Form Objects with Virtus](http://hawkins.io/2014/01/form_objects_with_virtus/)
* [Creating Form Objects with ActiveModel and Virtus](https://webuild.envato.com/blog/creating-form-objects-with-activemodel-and-virtus/)
* [ActiveModel Form Objects](https://robots.thoughtbot.com/activemodel-form-objects)
* [**Reform**](https://github.com/trailblazer/reform)

Encapsulate logic related to validating and persisting data.

You can move validation to Form Object, but your model still need it just in case.

> So this isn't a SRP violation, they are two different responsibilities and relate to different chapters in the lifecycle of information.

```ruby
# At the controller
@company_form = CompanyForm.new(company_params)

# The form object
class CompanyForm
  include ActiveModel::Model

  validates :name, presence: true
  validates :number, presence: true
  validate :validate_company_and_phone
  
  # Act as the parent object
  def self.model_name
    Company.model_name
  end
  
  def save
    return unless valid?
    ActiveRecord::Base.transaction do
      company.save!
      phone.save!
    end
  end
  
  private
  
  def company
    @company ||= Company.new(name: name)
  end
  
  def phone
    @phone ||= @company.phones.build(number: number, primary: true)
  end
  
  def validate_company_and_phone
    return display_errors(company.errors) if company.invalid?
    return display_errors(phone.errors) if phone.invalid?
  end
  
  # Bubble error from child relationship up to the parent
  def display_errors(errors)
    errors.each do |attribute, message|
      errors.add(attribute, message)
    end
  end
end
```

## Value Object (Immutable)

* [tcrayford/Values](https://github.com/tcrayford/Values)
* [To Clojure and back](https://www.youtube.com/watch?v=doZ0XAc9Wtc)

Simple, small object that represents certain value-ness instead of an identity. Examples are money values in various currencies, temperatures, etc.

Conversion and comparison of values is one of the function Value object can perform reliably.

Anytime you need to do immutable conversion or comparison, you can consider encapsulate those logics into Value object.

```ruby
class Temperature
  include Comparable
  SCALES = %w(:kelvin :celsius)
  
  attr_reader :degrees, :scale, :kelvin_degrees
  
  def initialize(degrees, scale = :kelvin)
    @degrees = degrees.to_f
    @scale = case scale
    when *SCALES then scale
    else :kelvin
    end
    
    @kelvin_degrees = case @scale
    when :kelvin
      @degrees
    when :celsius
      @degrees + 273.15
    end
  end
  
  def self.from_celsius(degrees)
    new(degrees, :celsius)
  end
  
  def self.from_kelvin(degrees)
    new(degrees, :kelvin)
  end
  
  def <=>(other)
    kelvin_degrees <=> other.kelvin_degrees
  end
end
```

## Query Object

As much as possible use ActiveRecord scopes or class methods to generate query. Do not do the query inside controller.

> I find that scopes are best used when they're simple and don't do too much. I think of them as reusable building blocks. If I need to do something more complicated, I used a Query class to encapsulate the potentially gnarly query.

```ruby
class VolunteersNotMemberQuery
  def initialize(year:)
    @year = year
  end
  
  def relation
    volunteer_ids = GroupMembership.select(:person_id).school_year(@year)
    pta_member_ids = PtaMembership.select(:person_id).school_year(@year)
    
    Person
      .active
      .adults
      .where(id: volunteer_ids) # Will become sub-query
      .where.not(id: pta_member_ids)
      .order(:last_name)
  end
end
```

## View Object

* [Draper](https://github.com/drapergem/draper)

A.k.a Serializer or Presenter

Good when you want to represent JSON response or HTML view. This is especially helpful when you have controller and model information like `articles_path` URL to show to the user.

## Policy Object

If you want to enforce policy like who has permission to create resources, how many resources can be created, who can view what, you need Policy Object. Policy Objects are interchangeable. They can be replaced depending on access level or other context.

Move the policy checking out of the controller and model.

```ruby
class CreateInvoicePolicy
  def initialize(user)
    @user = user
  end
  
  def allowed?
    @user.finance? && !blocked
  end
  
  private
  
  def blocked
  end
end

class InvoiceController < ApplicationController
  def create
    if policy.allowed?
      InvoiceService.new(invoice_params)
    else
      head :unauthorized
    end
  end
  
  private
  
  def policy
    CreateInvoicePolicy.new(current_user)
  end
end
```

## Decorator

* [Strategy vs Decorator](https://www.google.com.sg/webhp?sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#q=decorator%20vs%20strategy)

---

* If you have many actions to cover
* When you want to add more auxiliary behavior to individual object without affecting other objects of the same class
* Format complex data for display

## Batch Processing

* [Ruby BatchLoader](https://engineering.universe.com/batching-a-powerful-way-to-solve-n-1-queries-every-rubyist-should-know-24e20c6e7b94)

```ruby
# 5.1 add support for limits in batch processing
Post.limit(500).find_each.map(&:title)
```