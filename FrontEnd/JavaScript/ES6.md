# ES6

https://github.com/Chalarangelo/30-seconds-of-code

* [JS Essentials](https://codeburst.io/javascript-essentials-numbers-and-math-72655b2e5edd)
* [33 concepts every JavaScript developer should know](https://github.com/leonardomso/33-js-concepts)
* [How JavaScript works - A series](https://blog.sessionstack.com/how-javascript-works-the-building-blocks-of-web-workers-5-cases-when-you-should-use-them-a547c0757f6a)
* [**The Modern JavaScript Tutorial**](https://javascript.info/)
* [Understanding ECMAScript 6 - Nicholas C. Zakas](https://leanpub.com/understandinges6/read)
* [Exploring ES6 - Dr. Axel Rauschmayer](http://exploringjs.com/es6/index.html)
* [Exploring ES2016 and ES2017 - Dr. Axel Rauschmayer](http://exploringjs.com/es2016-es2017/index.html)
* [ES2015+ Cheatsheet](https://devhints.io/es6)
* [JavaScript Object Explorer - Find the object method you need without digging through the docs](https://sdras.github.io/object-explorer/)
* [ES modules: A cartoon deep-dive](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/)
* [Interview questions?](https://medium.freecodecamp.org/the-definitive-javascript-handbook-for-a-developer-interview-44ffc6aeb54e)
* [A guide to JavaScript Regular Expressions](https://flaviocopes.com/javascript-regular-expressions/)
* [JavaScript "Prototype Chains"](https://medium.com/@hyejunglim/javascript-prototype-chains-cff594f35431)
* [Mastering Modular JavaScript](https://github.com/mjavascript/mastering-modular-javascript)

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

## Execution Context

* [Understanding Execution Context and Execution Stack in Javascript](https://blog.bitsrc.io/understanding-execution-context-and-execution-stack-in-javascript-1c9ea8642dd0)

## Conditionals

* [5 yips to write better conditionals](https://scotch.io/bar-talk/5-tips-to-write-better-conditionals-in-javascript)

## Let

* `var`-variables don't have Temporal Dead Zone. When the scope (its surrounding function) of a `var` variable is entered, storage space (a binding) is created for it. The variable is immediately initialized, by setting it to `undefined`.
* `let`-variables have Temporal Dead Zone.

`let` hoist but it does not do initialization.

```js
// You can see the dead zone is really temporal (based on time)
// and not spatial (based on location)
let foo = console.log(foo); // ReferenceError due to TDZ

if (true) { // enter new scope, TDZ starts
  const func = function() {
    console.log(myVar); // OK!
  }
  
  let myVar = 3; // TDZ ends
  func(); // called outside TDZ
}
```

## Function Parameters

* [Best practices for JavaScript function parameters](https://codeutopia.net/blog/2016/11/24/best-practices-for-javascript-function-parameters/)
* [Require Parameters for JavaScript Functions](https://davidwalsh.name/javascript-function-parameters)
* [Function Parameters in Detail](https://blogg.bekk.no/function-parameters-in-detail-b0f0d971bec3)

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

// Don't anyhow use arrow function at event handler
const box = document.querySelector('.box')
box.addEventListener('click', () => {
  // `this` will not be the box, but rather the
  // global window object
  // You are better off using normal function()
  console.log(this)
})

// To fix the above, we usually use normal function
// at the top of the parent
const box = document.querySelector('.box')
box.addEventListener('click', function() {
  // this refer to the box
  this.classList.toggle('opening')
  setTimeout(() => {
    // with arrow-function, this also refer to
    // the box
    this.classList.toggle('open')
  }, 500)
})
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

* [Modules Modules Modules - The difficulty of CJS and ESM](https://www.youtube.com/watch?v=W5CXzo4TZVU)
* [JavaScript Module System](http://exploringjs.com/es6/ch_modules.html)
* [ES6 Modules in Depth](https://ponyfoo.com/articles/es6-modules-in-depth#the-es6-module-system)
* [The JavaScript Modules Limbo](https://codeburst.io/the-javascript-modules-limbo-585eedbb182e)
* [`import * as React` vs `import React`](https://discuss.reactjs.org/t/es6-import-as-react-vs-import-react/360/9)
* [Misunderstanding ES6 Modules, Upgrading Babel, Tears, and a Solution](https://blog.kentcdodds.com/misunderstanding-es6-modules-upgrading-babel-tears-and-a-solution-ad2d5ab93ce0)
* [ES6: The Bad Parts](https://benmccormick.org/2018/06/05/es6-the-bad-parts/)

```js
export default {
  red: '#ff4433',
  yellow: '#ffdc00'
}

import { red, yellow } from './colors'
```

### Named Import

Note that named import still import the entire library:

```js
// Still import *everything* in my-component
// and bloats bundle! Need index.js at root also.
import { Label } from 'my-component';

// Bootstrap optimize bundle size by using /lib
import Button from 'react-bootstrap/lib/Button';
```

## Tree Shaking

* Use `export { default as XX }` for easier ES6 imports and tree shaking
* [Why we have banned default exports in Javascript and you should do the same](https://blog.neufund.org/why-we-have-banned-default-exports-and-you-should-do-the-same-d51fdc2cf2ad)

```js
// It is always easier to do this and expect tree shaking to only
// import the 2 functions
import { isEmail, isNumeric } from 'validator';

// In order to do this, we need to export it using...
export { default as isEmail } from './lib/isEmail';
export { default as isNumeric } from './lib/isNumeric';

// Please verify!
// Normally this won't work with tree shaking, but is it because
// we are using export default as first?
// Don't think need this...
export default { isEmail, isNumeric }
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
  
  // Also class property, but instance property
  x = 'bar'
  
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
* [Taming `this` In JavaScript With Bind Operator](https://www.smashingmagazine.com/2018/10/taming-this-javascript-bind-operator/)

## Gather/Rest and Spread Operators

Spread unpack items insides array/object and gather/rest package items into a single unit.

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

function foo(...args) { // Rest parameter "gather" into an array
  args.unshift(42)
  bar(...args) // Spread out the array into individual parts
}

function foo(...args) {
  bar(42, ...args) // even more simple
}
```

Gather (pack) and spread (unpack) is nice opposite of each other.

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

Think of it as the opposite of constructing where we create data, while destructuring is where we extract data.

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

// x = 'a'
// y = 'b'
// z = 'c'
// You can use pattern for the rest operator also
const [x, ...[y, z]] = ['a', 'b', 'c']
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

```js
// It is like accessing the 'abc'.length property
const { length: len } = 'abc' // len=3

// Object destructuring for array items
const csv = '1997,John Doe,US,john@doe.com,New York'
const { 2: country, 4: state } = csv.split(',')
```

Another benefit of destructuring object is immutability:

https://medium.com/@yurik1776/hey-bill-569e596030b7

```js
const options = {
  role: 'Admin'
}

let { role } = options // Making a shallow copy
role = role.toLowerCase() // 'admin'

options.role // still 'Admin', did not mutate!
```

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

* [Arrays, symbols, and realms](https://jakearchibald.com/2017/arrays-symbols-realms/)
* [JavaScript Symbols, Iterators, Generators, Async/Await, and Async Iterators — All Explained Simply](https://medium.freecodecamp.org/some-of-javascripts-most-useful-features-can-be-tricky-let-me-explain-them-4003d7bbed32)

All not that useful in a general case. A unique unguessable value. Use it as a symbolic placeholder for "something".

## Iterator

```js
// A new iteration is a brand new block, so we can use const
// args.entries() give you index to loop over
for (const [index, elem] of args.entries()) {
}
```

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

// Remove duplicate items from an array using Set with spread operator
[...new Set([1, 1, 1, 1, 22, 3, 2, 2])]
```

## History

Players:

* Google
* Mozilla
* Microsoft
* Apple
* Adobe
* Opera
* Yahoo

---

* JavaScript 1.5
* JavaScript 2.0 = ECMAScript 4

## Videos

* [Untangle your code with yield](https://www.youtube.com/watch?v=B15sTBSAotk)
* [JavaScript Patterns for 2017](https://www.youtube.com/watch?v=hO7mzO83N1Q)

