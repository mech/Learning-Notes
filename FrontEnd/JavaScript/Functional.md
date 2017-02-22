# Functional JavaScript

2 models of computations:

1. Alonzo Church - Lambda calculus is a universal model of computation based on function composition.
2. Alan Turing - Turing machine is a universal model of computation that defines a theoretical device that manipulate symbols on a strip of tape.

---

* [Eliminate the switch statement](https://hackernoon.com/rethinking-javascript-eliminate-the-switch-statement-for-better-code-5c81c044716d#.7btlwolac)
* [The Rise and Fall and Rise of Functional Programming - A Series (Must read)](https://medium.com/javascript-scene/the-rise-and-fall-and-rise-of-functional-programming-composable-software-c2d91b424c8c#.7ourrkni2)
* [Curry or Partial Application?](https://medium.com/javascript-scene/curry-or-partial-application-8150044c78b8#.fxhqqauo2)
* [Currying - the Underrated Concept in Javascript](https://medium.com/@iquardt/currying-the-underestimated-concept-in-javascript-c95d9a823fc6#.n1jqb68ju)

```js
// Functions can be anonymous
add(x, y) => x + y
(x, y) => x + y

// Function in λ only accept a single input. They are unary.
// If you need more than one parameter, use currying
(x, y) => x + y

// Becomes
x => y => x + y

// Composition
f . g

compose2 = f => g => x => f(g(x))
```