# ES6

* [Understanding ECMAScript 6 - Nicholas C. Zakas](https://leanpub.com/understandinges6/read)
* [Exploring ES6 - Dr. Axel Rauschmayer](http://exploringjs.com/es6/index.html)
* [Exploring ES2016 and ES2017 - Dr. Axel Rauschmayer](http://exploringjs.com/es2016-es2017/index.html)
* [ES2015+ Cheatsheet](https://devhints.io/es6)

---

* [**Practical Modern Javascript**](https://github.com/mjavascript/practical-modern-javascript)
* [Clean Code for JavaScript](https://github.com/ryanmcdermott/clean-code-javascript)
* [Optimization killers](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)
* [Polyfills: everything you ever wanted to know, or maybe a bit less](https://hackernoon.com/polyfills-everything-you-ever-wanted-to-know-or-maybe-a-bit-less-7c8de164e423#.1wg5unfwr)
* [Nice tutorial on ES6 with React](http://www.benmvp.com/slides/2017/reactconf/react-esnext.html#/)
* [Introduction to commonly used ES6 features](https://zellwk.com/blog/es6/)
* [Overview of ECMAScript 6 features](https://github.com/lukehoban/es6features)
* [What Do I Need to Know to Ace a JavaScript Interview?](https://github.com/adam-s/js-interview-review)
* [The Best Frontend JavaScript Interview Questions (written by a Frontend Engineer)](https://performancejs.com/post/hde6d32/The-Best-Frontend-JavaScript-Interview-Questions-(Written-by-a-Frontend-Engineer))
* [What the f*ck JavaScript?](https://github.com/denysdovhan/wtfjs)
* [Pretty algorithms - Common useful algorithms written in modern JavaScript](https://github.com/jiayihu/pretty-algorithms)

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

## Let

`let` hoist but it does not do initialization.

## Function Parameters

* [Best practices for JavaScript function parameters](https://codeutopia.net/blog/2016/11/24/best-practices-for-javascript-function-parameters/)
* [Require Parameters for JavaScript Functions](https://davidwalsh.name/javascript-function-parameters)

## Arrow Function

* [When should I use Arrow Functions? - James K Nelson](https://reactarmory.com/answers/when-to-use-arrow-functions)

```js
// Never use arrow functions to declare object methods as you
// can't reference the object with `this`
let o = {
  notThis: () => {
    console.log(this) // window
  },
  
  doThis() {
  }
}

// Be careful that you're always keeping scope in mind. Arrow
// functions do not block off the scope of `this`
var tahoe = {
  resorts: ['Kirkwood', 'Squaw', 'Alpine'],
  
  // No error
  goodPrint: function(delay=1000) {
    setTimeout(() => {
      console.log(this.resorts.join(','))
    }, delay)
  },
  
  // Error!
  // Cannot read property resorts of undefined
  badPrint: (delay=1000) => {
    setTimeout(() => {
      console.log(this.resorts.join(','))
    }, delay)
  }
}
```

```js
// Cannot re-bind with bind, apply, or call

const adder = {
  sum: 0
}

const add = (numbers) => numbers.forEach(n => this.sum += 1)

adder.add = add.bind(adder)

adder.add([1, 2, 3])
```

## Module Export Import

* [JavaScript Module System](http://exploringjs.com/es6/ch_modules.html)
* [ES6 Modules in Depth](https://ponyfoo.com/articles/es6-modules-in-depth#the-es6-module-system)
* [The JavaScript Modules Limbo](https://codeburst.io/the-javascript-modules-limbo-585eedbb182e)

```js
export default {
  red: '#ff4433',
  yellow: '#ffdc00'
}

import { red, yellow } from './colors'
```

## Classes

* [Classes in ECMAScript 6 (final semantics)](http://2ality.com/2015/02/es6-classes-final.html)
* [ESnext class features for JavaScript](https://github.com/tc39/proposal-class-fields)

## React

```js
class Button extends React.Component {
  // Actually you do not need constructor and call super(props)
  // unless you need to use this.props inside the constructor
  constructor(props) {
    super(props)
    
    this.state = {
    }
    
    // Binding option 1
    this.handleClick = this.handleClick.bind(this)
  }
  
  // Class properties
  state = {
  }
  
  // Static properties
  static propTypes = {
  }
  
  static defaultProps = {
  }
  
  // Binding option 2 and better with lexical scoping using arrow function
  // Bound instance property functions
  // It looks like a method, but it is not. It really is just an instance property.
  // Thus, when subclassing, this handleClick will not be inherited
  handleClick = () => {
  }
  
  // With async
  handlePressAsync = async () => {
    if (!await Connectivity.isAvailableAsync()) {
      this.alertNoInternetConnection()
    }
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

```js
// ...restProps will pull out all of the props that hasn't
// been pulled out
const Greeting = ({ name, punc, ...restProps }) =>
  <h1 {...restProps}>Hello, {name}(punc)</h1>
```

```js
button: {
  borderRadius: 2,
  ...Platform.select({
    ios: {
      backgroundColor: IOS_BLUE
    },
    android: {
      backgroundColor: MATERIAL_BLUE,
      elevation: 3
    }
  })
}
```

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

function foo([first, ...rest]) {
}
foo([1, 2, 3])

var a = [1, 2, 3]
var b = [4, 5, 6]

foo(...a, ...b) //=> [3, 4, 5, 6]

// ...a and ...b will spread out into individual part
// x = 1
// y = 2
// rest = [3, 4, 5, 6]
// rest gather the rest of the argument into an array
foo(1, 2, 3, 4, 5, 6)

// Spread is just like concat
var arr = [1, 2, 3]
var newArr = [ ...arr ]
var same = [].concat(arr)
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

## Tips

```js
// don't write this:
if (obj.props) {} // could be 0, "", null...

// if you mean this:
if (obj.props !== undefined) {} // Explicit and faster
```

## Videos

* [Untangle your code with yield](https://www.youtube.com/watch?v=B15sTBSAotk)
* [JavaScript Patterns for 2017](https://www.youtube.com/watch?v=hO7mzO83N1Q)