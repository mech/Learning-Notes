# ES6

* [Clean Code for JavaScript](https://github.com/ryanmcdermott/clean-code-javascript)
* [Optimization killers](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)
* [Polyfills: everything you ever wanted to know, or maybe a bit less](https://hackernoon.com/polyfills-everything-you-ever-wanted-to-know-or-maybe-a-bit-less-7c8de164e423#.1wg5unfwr)
* [Nice tutorial on ES6 with React](http://www.benmvp.com/slides/2017/reactconf/react-esnext.html#/)

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

## React

```js
class Button extends React.Component {
  constructor(props) {
    super(props)
    
    this.state = {
    }
    
    // Binding option 1
    this.handleClick = this.handleClick.bind(this)
  }
  
  render() {
  }
}

// Safe way if we do not want to depend on Class Properties (Draft stage)
Button.propTypes = {
}

Button.defaultProps = {
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

## Destructuring

Kind of like pattern matching, but not really.

### Array Destructuring

```js
var array = [1, 2, 3]

// We can have default value and gather/rest operator
// a = 1
// b = 2
// c = 3
// d = 42
// e = undefined
// args = []
var [a, b, c, d = 42, e, ...args] = array || []
```

```js
var a = [1, 2, 3]

// Throwing away first 2 elements [0, 1] and then gather the rest
// and re-assign to `a`
[, , ...a] = [0, ...a, 4] // => [2, 3, 4]
```

**Nested array destructuring**

```js
var a = [1, 2, 3, [4, 5, 6]]

// args = [[4, 5, 6]] which may not be what you want
var [a, b, c,...args] = a

// d = 4
// e = 6
var [a, b, c, [d, , e]] = a
```

### Object Destructuring

Mimic named arguments pattern somehow.

## Tag Functions

```js
function upper(strings, ...values) {
  var str = '';
  for (var i=0; i<strings.length; i++) {
    if (i > 0) str += values[i-1].toUpperCase()
    str += strings[i]
  }
  
  return str
}

// usage
upper`Hello ${name}`
```

## Symbols

All not that useful in a general case. A unique unguessable value. Use it as a symbolic placeholder for "something".

## Iterator

```js
Array.prototype[Symbol.iterator] = function* () {
  for (let i = 0; i < this.length; i++) {
    yield this[i];
  }
}

// Using for-of
for (const elem of ['a', 'b', 'c']) {
  console.log(elem);
}
```

```js
class TupleArray extends Array {
  *[Symbol.iterator]() {
    for (let i = 0; i < this.length; i++) {
      yield [i, this[i]];
    }
  }
}

// Will return tuples
// [0, 'a']
// [1, 'b']
// [2, 'c']
```

```js
Number.prototype[Symbol.iterator] = function* () {
  let i = 0;
  while (i < this) { // Notice the this here
    yield i++;
  }
}

// Using spread operator directly on a number primitive
console.log(...5);
```

Iterables implement `[Symbol.iterator]()`

Iterators implement `next()` and `throw()`

## Object Getter

```js
get canShowSecretData() {
  return dataIsReady && isAdmin
}

get price() {
  return `${this.props.currency}${this.props.value}` 
}

render() {
  return (
    <div>
      {this.canShowSecretData && <SecretData />}
    </div>
  )
}
```

## Async Await

* `await` takes in any Promises
* Use normal try-catch to handle exceptions

```js
async submitForm(data) {
  try {
    let res = await fetch(url, {
      method: 'POST',
      body: JSON.stringify(data)
    })
    
    newData = await res.json()
  } catch(err) {
    // handle error
  }
  
  this.setState({ data })
}
```

## Videos

* [Untangle your code with yield](https://www.youtube.com/watch?v=B15sTBSAotk)