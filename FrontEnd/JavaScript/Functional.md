# Functional JavaScript

In functional programs, we should use functions over values wherever possible:

```js
const oneSecond = () => 1000
const getCurrentTime = () => new Date()
const clear = () => console.clear()
```

> Functions are treated no differently than data. Function is data.

2 models of computations:

1. Alonzo Church - Lambda calculus is a universal model of computation based on function composition.
2. Alan Turing - Turing machine is a universal model of computation that defines a theoretical device that manipulate symbols on a strip of tape.

---

* [Why using .chain is a mistake](https://medium.com/making-internets/why-using-chain-is-a-mistake-9bc1f80d51ba)
* [Eliminate the switch statement](https://hackernoon.com/rethinking-javascript-eliminate-the-switch-statement-for-better-code-5c81c044716d#.7btlwolac)
* [The Rise and Fall and Rise of Functional Programming - A Series (Must read)](https://medium.com/javascript-scene/the-rise-and-fall-and-rise-of-functional-programming-composable-software-c2d91b424c8c#.7ourrkni2)
* [Curry or Partial Application?](https://medium.com/javascript-scene/curry-or-partial-application-8150044c78b8#.fxhqqauo2)
* [Currying - the Underrated Concept in Javascript](https://medium.com/@iquardt/currying-the-underestimated-concept-in-javascript-c95d9a823fc6#.n1jqb68ju)
* [Learn the fundamentals of functional programming](https://medium.freecodecamp.com/learning-the-fundamentals-of-functional-programming-425c9fd901c6#.qchw5q8go)
* [Writing Elegant Code With React, Redux and Ramda](https://medium.com/javascript-inside/the-elegance-of-react-ebc21a2dcd19)
* [Functional Programming Jargon](https://github.com/hemanth/functional-programming-jargon)
* [Learn FP with React](https://jaysoo.ca/2017/04/30/learn-fp-with-react-part-1/)
* [How I rediscovered my love for JavaScript after throwing 90% of it in the trash e](https://hackernoon.com/how-i-rediscovered-my-love-for-javascript-after-throwing-90-of-it-in-the-trash-f1baed075d1b)

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

## Higher-Order Functions

```js
var createScream = function(logger) {
  return function(message) {
    logger(message.toUpperCase() + '!!!')
  }
}

const scream = createScream(message => console.log(message))

scream('functions can be returned from other functions')

// Or using arrow functions
const createScream = logger => message =>
  logger(message.toUpperCase() + '!!!')
```

More than one arrow means that we have a higher-order function.

## Currying

Currying is a functional technique that involves the use of higher-order functions. Currying is the practice of holding on to some of the values needed to complete an operation until the rest can be supplied at a later point in time. This is achieved through the use of a function that returns another function, the curried function.

```js
// Here userLogs is a higher-order function.
const userLogs = userName => message =>
  console.log(`${userName} -> ${message}`)
  
// The log function is produced from userLogs and thus was curried.
const log = userLogs('mech')

log('attempted to load')
```

## flatMap

* [Functional pattern: flatMap](http://2ality.com/2017/04/flatmap.html)

## Functor

* [Functors & Categories](https://medium.com/javascript-scene/functors-categories-61e031bac53f#.gug709a8t)

A functor is something that can be mapped over. It's a container that is "mappable".

Array and Promises are functors. Interesting `.then()` obeys the functor laws.