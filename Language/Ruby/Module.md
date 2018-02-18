# Module in Ruby

Modules are a form of inheritance in Ruby.

## Rails Concern

Bad concern:

* Purely cosmetic, the responsibilities are still there
* By using concern, we lose explicitness
* Harder to test, since you need more arrangement
* Is actually a form of inheritance rather than composition
* Encourage is-a relationship rather than has-a relationship

A good concern:

* Able to work in isolation, must be dependency-free
* Should have a very concrete and limited responsibility
* Responsibility should be framework or infrastructure related. They shouldn't contain business logic. Business logic is better modelled as abstraction (classes), rather than concerns.

It is hard to say what problem concerns solve. Every problem that concerns solve can be solved with composition or aggregation. Better than that, composition/aggregation solve the same problem but **explicitly**.

> Explicit is better than implicit

Framework can use concerns. But business logics better use normal classes and composition.

