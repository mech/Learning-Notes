# ES6

* [Clean Code for JavaScript](https://github.com/ryanmcdermott/clean-code-javascript)
* [Optimization killers](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)

Encapsulate conditionals:

```js
// Bad
if (fsm.state === 'fetching' && isEmpty(listNode)) {
}

// Good
function shouldShowSpinner(fsm, listNode) {
  return fsm.state === 'fetching' && isEmpty(listNode)
}

if (shouldShowSpinner(fsm, listNode)) {
}
```

## this

* [Understanding JavaScript Function Invocation and "this"](http://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/)

## Gather/Rest and Spread Operators

There are 3 different "spread" operators in JavaScript:

1. Array spreads, which is part of ES6
2. Object spreads, which are currently a Stage 3
3. JSX spreads

### Gather/Rest

```js
function foo() {
  var args = [].slice.call(arguments)
  args.unshift(42)
  bar.apply(null, args)
}

function foo(...args) { // Gather into an array
  args.unshift(42)
  bar(...args) // Spread out the array into individual parts
}

function foo(...args) {
  bar(42, ...args) // even more simple
}
```

Gather and spread is nice opposite of each other.

Array can be spread out in function call as well as assignment:

```js
var x = [0, ...a, ...b, 7]
```

```js
function foo(x, y, ...rest) {
  return rest
}

var a = [1, 2, 3]
var b = [4, 5, 6]

foo(...a, ...b) //=> [3, 4, 5, 6]

// ...a and ...b will spread out into individual part
// x = 1
// y = 2
// rest = [3, 4, 5, 6]
// rest gather the rest of the argument into an array
foo(1, 2, 3, 4, 5, 6)
```