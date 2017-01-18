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

## Spread Operators

There are 3 different "spread" operators in JavaScript:

1. Array spreads, which is part of ES6
2. Object spreads, which are currently a Stage 3
3. JSX spreads