# Clean Architecture

> The primary purpose of architecture is to support the life cycle of the system.
> 
> ---
> 
> A good architecture maximises the number of decisions NOT made

## Story

Story of your domain. Metaphor. Tell your story and explore it.

Your domain model is not in your classes, it's in the **communication patterns between the objects at runtime**.

You can either design your model around data or around their responsibilities (things they have to do).

## Boundaries

It is easy to see hardware boundaries. Software boundaries are just harder to see and separate.

## Case Study: Claim Validation

**What is behavior?**

Clearly, submitting of claim is behavior. Checking the claims is a behavior. Notifying contractor on the status of claims is behavior.

Who is responsible for notifying? Who is responsible for checking?

Where's the behavior assembly system?

"Tell, don't ask". Your Rails controller will have many procedural code.

The behavior can become a Use Case and conduct business function like "Submit Claims".

Use case is also Command Pattern, Service Object, Actions, etc.

**What is data?**

A safe place to store all the receipts.

## Videos

* [GoRuCo 2012 Hexagonal Rails by Matt Wynne](https://www.youtube.com/watch?v=CGN4RFkhH2M)