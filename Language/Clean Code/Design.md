# Object Oriented Design

> Working code pay the bill

> Write the usage code first

* [The Unofficial Guide to Rich Hickey's Brain](http://www.flyingmachinestudios.com/programming/the-unofficial-guide-to-rich-hickeys-brain/)
* [Software Engineering Blogs](https://github.com/kilimchoi/engineering-blogs)
* [Code Show and Tell: PolymorphicFinder](https://robots.thoughtbot.com/code-show-and-tell-polymorphic-finder)
* [How We Ship: Codetree](https://codetree.com/how-we-ship/interviews/codetree)
* [How To Understand The Balance Between Learning And Progress](https://hackernoon.com/how-to-understand-the-balance-between-learning-and-progress-6783e7f711ac)
* [Naming: The hardest problem in computer science](https://eev.ee/blog/2016/07/26/the-hardest-problem-in-computer-science/)
* [Goodbye, Object Oriented Programming](https://medium.com/@cscalfani/goodbye-object-oriented-programming-a59cda4c0e53)

Good code not only works, but is also simple, understandable, expressive and changeable.

Good design preserves maximum flexibility at minimum cost by putting off decisions at every opportunity, deferring commitments until more specific information arrive.

> We propose instead that one begins with a list of difficult design decisions or **design decisions which are likely to change**.
> 
> Each module is then designed to **hide such a decision from the others**.

## Boundaries

* Ubiquitous language within the bounded context
* Strategic modeling
* With Ubiquitous Language and Subdomains
* We want limits. We want boundaries. We want borders.
* Boundaries have to be tangible.
* Crossing the boundary should be a bit harder than operating within the limits of it.
* Allows us to break things into pieces.
* [Bring clarity to your monolith with Bounded Contexts](https://blog.carbonfive.com/2016/11/01/bring-clarity-to-your-monolith-with-bounded-contexts/)

---

* Just large enough - knows its boundaries
* Highly cohesive and loosely coupled
* Don't couple directly to the task-based UI
* Precise semantics that fully express the business domain
* [Domain Event](https://blog.carbonfive.com/2017/07/18/evented-rails-decoupling-complex-domains-in-rails-with-domain-events/)

> Ask yourself: what do these columns have in common? Why have they landed in the same database table and ActiveRecord model? Is it because they are **updated on the same screen**?

> At a certain point however, the complexity of your domain increases and a one-to-one mapping between screen UIs and database design (and ActiveRecord models) is no longer good enough.

## Entities

Entities are **Enterprise Business Rules**. Entities include business rules that are universal to a company. They represent entities that are basic to its area of operation. They are the components with the **highest level of abstraction**.

## Use Cases

Use Cases are pointed out as **Application Business Rules**.

An element in the Use Cases layer can't have any knowledge about any class or module related to GUI or data persistence. Likewise, an Entity can't know which Use Cases make use of it.

Entities are blissfully unaware of which Use Cases are using them.

## Aggregates

* Tactical modeling
* With Domain Events

Classes with attributes that cooperate together and need to be updated in one transaction to protect business rules are called Aggregates.

The role of an aggregate is to protect business rules, to protect invariants.

## Event Sourcing

* Modelling events forces temporal focus - Event force you to think temporally
* Structure vs Behavioral - Events improve behavioral factor of your system
* Append-only log
* Kafka is event sourcing
* Flux is event sourcing
* Redux is event sourcing

## Policies

## Naming

Introduce new words into the application vocabulary.

New name is actually an opportunity to reveal intent. But more names also has its cognitive costs.

* Use case

Is it `CreateUser` or is it `RegisterUser`? `DeleteClass` or `DeregisterStudent`?

Is it `ChangeAddress`? Is there a difference between "Correcting an Address" and "Relocating the Customer"?

Naming in Domain is important!

## Lack of Design

Failure of OOD might look like failures of coding technique but they are actually failures of perspective.

> Gain design understanding
> 
> Exposing core concept. Unearth concepts that are currently hidden in the code.
> 
> Does extremely well on the domain questions

## Cost of Change

> Code that needs to be changed must be changeable. The code arrangement that was acceptable for Shameless Green is not necessarily best for "enabling change".

Something always change. It always does. The customers didn't know what they wanted, they didn't say what they meant. You didn't understand their needs, you've learned how to do something better, etc.

It is the need for change that makes design matter.

Dependencies stand in the way of change.

You must combine an overall understanding of your application's requirements with knowledge of costs and benefits of design alternatives and then devise an arrangement of code that is cost effective in the present and will continue to be so in the future.

Design that anticipate specific future requirements almost always end badly. Practical design does not anticipate what will happen to your application, it merely accepts that something will and that, in the present, you cannot know what.

## Principles and Patterns

* [Design Patterns for Humans!](https://github.com/kamranahmedse/design-patterns-for-humans)

OO designer has tools - principles and patterns.

## Overdesign

A little bit of knowledge is dangerous; as their knowledge increases, they design relentlessly. In an excess of enthusiasm they apply principles inappropriately and see patterns where none exist.

## Iterative

The iterative nature of Agile development allows design to adjust regularly and to evolve naturally.

You customers can't define the software they want before seeing it, so it's best to show them sooner rather than later. Thus software should be build in tiny increments, gradually iterating your way into an application that meets the customer's true need.

> If lack of a feature will force you out of business today it doesn't matter how much it will cost to deal with the code tomorrow.

That is the beauty of this technique. You don't have to know how to solve the whole problem in advance. The plan is to nibble away, one code smell at a time, in faith that the path to openness will be revealed.

## Intention and Implementation

> The distinction between intention and implementation allows you to understand a computation first in essence and later, if necessary, in detail. - Kent Beck

```ruby
# song is the intention and verses(99, 0) is the implementation
def song
  verses(99, 0)
end
```

## Abstraction

> Make visible the invisible and thus reveal core concepts.

---

> Expert can suggest abstraction that's just perfect, it is one of those things that you'll never discover yourself, but which is obvious in hindsight.

* [The Wrong Abstraction](http://www.sandimetz.com/blog/2016/1/20/the-wrong-abstraction)

> Your code is less concrete but more abstract - you've made it initially harder to understand in hopes that it will ultimately be easier to maintain.

OOD isn't free!

DRY is a great idea, but that doesn't mean it's free. The price you pay for DRYing out code is that the invoker of the new method no longer knows the implementation, only the message it should send. If you're willing to pay this price (i.e. being willingly ignorant of the actual behavior), the reward your reap is that when the behavior changes, you need alter your code in only one place.

Did you divid one large class into many small ones? You can now reuse the new classes independently of one another, but it's no longer obvious how they fit together for the original case.

Increasing the level of abstraction is not free!

Each of these design choices has costs, and it only makes sense to pay these costs if you also accrue some offsetting benefits. Design is thus about picking the right abstraction. If you choose well, your code will be expressive, understandable and flexible. If you get the abstraction wrong, your code will be convoluted, confusing and costly.

> Even with the best of intentions, abstractions are easy to get wrong.

Well-meaning programmers tend to over anticipate abstractions, inferring them prematurely from incomplete information. Early abstractions are often not quite right and therefore they create a catch-22. You can't create the right abstraction until you fully understand the code, but the existence of the wrong abstraction may prevent you from ever doing so. **This suggests that you should not reach for abstractions, but instead, you should resist them until they absolutely insist upon being created**.

> The code you write should meet 2 conflicting goals: It must remain concrete enough to be understood while simultaneously being abstract enough to allow for change.

There is a sweet spot that represents the perfect compromise between comprehension and changeability, and it's your job as a programmer to find it.

> This code is hard to understand because it is inconsistent and duplicative, and because it contains **hidden concepts that it does not name**.

Duplication of logic suggests that there are concepts hidden in the code that are not yet visible because they haven't been isolated and named.

> Code clarity is built upon names.

---

> The code gives the impression that its author feared that the logic for selecting or invoking a template would someday need to change, and so added levels of indirection in a misguided attempt to protect against that day. They did not succeed.

---

> Insufficient patience can hurt your chances of revealing the right abstractions.

---

> Shameless Green is clearly the best solution, yet almost no one writes it. It feels embarrassingly easy, and is missing many qualities that you expect in good code. It duplicates strings and contains **few named abstractions**.

---

> Clean code is ... full of crisp abstractions ...

It is cheaper to manage temporary duplication than to recover from incorrect abstractions. The resulting code might just be "good enough". The challenge comes when a change request arrives. Code that's good enough when nothing ever changes may well be code that's not good enough when things do.

> Do you have enough information to identify the correct abstraction? It may be best to duplicate the code and wait for better information in the meantime.

If you cannot correctly identify the abstraction there may not be one, and if no common abstraction exists then inheritance is not the solution to your design problem.

When abstractions are correct, code is easy to understand. But if you DRY with too much vigor, it can middy the waters. This suggests an insufficient understanding of the problem or working with **incomplete information**.

> Abstraction is the Core Concept. It is the named information thingy that you need.

## Coupling

* [Nice wiki article on coupling](https://en.wikipedia.org/wiki/Coupling_(computer_programming))

We can have low coupling if we design our public interfaces (API) sensibly. Limit the responsibilities along functionality. Only interact with simple and stable interface. Only depend on high cohesion interfaces where related functionalities are being bundled together.

## nil is unfriendly

* [The Tragedy of Maybe and Ruby](http://bendyworks.com/blog/tragedy-maybe-monad-ruby)
* [Rails Refactoring Example: Introduce Null Object](https://robots.thoughtbot.com/rails-refactoring-example-introduce-null-object)

---

* NullObject when nil is always handled the same way
* Exceptions when nil is always a bug
* Maybe when nil needs to be handled specially each time

```ruby
# BAD
# We are afraid that price will return nil
# We are not confident to directly send the right message to an
# object we know can receive this message
price = subscription.try(:price) || 0
credit_card.charge(price)
```

```ruby
class User
  def address
    @address || NullAddress.new
  end
end

class NullAddress
  def address
    'No street name on file'
  end
end
```

## Eliminate `if` and `switch`

```ruby
# When you see a parameter in a conditional, that's control coupling
# The fact that this method has an if in it has leaked out into client code
# Changes can now require changes in these clients
# This method is a split with 2 different methods
def save(should_run_validations=true)
  if should_run_validations
    run_validations
    persist
  else
    persist
  end
end
```

## Relationship of Different Pieces

Change ripple through the system.

## Fluent Interface, Chain of Responsibility

Fluent interfaces are good for query builder object. Maybe bad for business object?

* [Fluent Interfaces in Ruby ecosystem](http://blog.arkency.com/2017/01/fluent-interfaces-in-ruby-ecosystem/)
* [Fluent Interfaces Are Bad for Maintainability](http://www.yegor256.com/2018/03/13/fluent-interfaces.html)
* [Fluent Interfaces are Evil](https://ocramius.github.io/blog/fluent-interfaces-are-evil/)

## Locality

Dependencies locality.

## Inheritance

> Inheritance is specialization

Use it for *is-a* relationship. Always have a shallow, narrow hierarchy rather than a deep, wide hierarchy.

## Compositionality

Decorator is just a form of object composition.

> The meaning of a compound expression is a function of the meanings of its parts and the syntactic rule by which they are combined. - [Building on SOLID foundations - Steve Freeman & Nat Pryce](https://www.youtube.com/watch?v=6Bia81dI-JE)

DSL can be composable. Is fluent language bad?

```java
Scenario bankingCrisis = ScenarioDefinition.create()
  .yieldCurveShifts(
    when(currency,
      is(EUR, proportionalShift(-0.1)),
      is(GBP, proportionalShift(-0.05)),
      is(USD, proportionalShift(+0.1)),
      otherwise(proportionalShift(+0.005))))
  .stockPriceShifts(
    when(sector, is(BANKING)))
```

```java
List<Employee> newEmployees = employees.hired(TODAY);

assertThat(newEmployees).hasSize(6).contains("frodo", "sam");
```

## Dependency Direction

Depend on things that change less often than you do.

Depending on an abstraction is always safer than depending on a concretion because by its very nature, the abstraction is more stable.

```ruby
class Sales < Persistence
  def self.total(within:)
    where(date: within).sum('cost')
  end
end

class Foo
  def sales_total(params, model=Sale)
    range  = DateRange.new(starting: params[:starting], ending: params[:ending]).range
    model.total(within: range)
  end
end

class TotalizableDouble
  def self.total(within:)
    47
  end
end

class FooTest < MiniTest::Test
  def test_sales_total
    params = {starting: '2016-04-01', ending: '2016-04-07'}
    model = TotalizableDouble
    assert_equal 47, Foo.new.sales_total(params, model)
  end
end
```

## Open/Closed Principle

The decision about whether to refactor in the first place should be determined by whether your code is already "open" to the new requirement.

Code is open to a new requirement when you can meet that new requirement without changing existing code.

If you're unclear how to make code open, the way forward is to start removing code smells.

## Liskov Substitution Principle

```ruby
number.to_s.capitalize
```

## Interface Segregation Principle

* [Avoiding Interface Pollution with the Interface Segregation Principle](https://medium.com/@severinperez/avoiding-interface-pollution-with-the-interface-segregation-principle-5d3859c21013) 

In Ruby, we do not have interface types. We are not forced into implementing anything. So "fat interface pollution" is not in Ruby.

But we can still pollute method interface "signature", like:

```ruby
def find_all_post(category:)
end

def find_all_post(category:, sort: false)
end

# Or should we just create another method interface
def find_all_post_sorted(category:, sort:)
end
```

## The Flocking Rules

* [The Scandalous Story of the Dreadful Code Written by the Best of Us](https://www.youtube.com/watch?v=-wYLmsizBc0)

## Unit and Integration Testing

* [Falling through the KRACKs](https://blog.cryptographyengineering.com/2017/10/16/falling-through-the-kracks/)

