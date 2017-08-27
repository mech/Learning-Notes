# Immutability

String and numbers are always immutable by default. However, in Redux, state is almost always represented as an object.

Ideally we want `shouldComponentUpdate` to always return `false`, but that is not realistic. So the next best option is to do simple and fast equality check.

Equality check for value like string, boolean and integer is simple. Equality check for objects, arrays and functions is problematic.

Immutable.js allows us to detect changes in JavaScript objects/arrays without resorting to the inefficiencies of deep equality checks, which in turn allows React to avoid expensive re-render operations when they are not required.

* [Handling State in React: Four Immutable Approaches to Consider](https://medium.com/@housecor/handling-state-in-react-four-immutable-approaches-to-consider-d1f5c00249d5)
* [How To Use Immutable.js in a React Redux Application](https://codebrahma.com/how-to-use-immutable-js-in-a-react-redux-application/)
* [React, Redux and Immutable.js: Ingredients for Efficient Web Applications](https://www.toptal.com/react/react-redux-and-immutablejs)
* [updeep - Easily update nested frozen objects and arrays in a declarative and immutable manner](https://github.com/substantial/updeep)
* [Immutable Data Structures and JavaScript](http://jlongster.com/Using-Immutable-Data-Structures-in-JavaScript)
* [Pros and Cons of using immutability with React.js](http://reactkungfu.com/2015/08/pros-and-cons-of-using-immutability-with-react-js/)

A `const` object can't be reassigned to refer to a completely different object, but the object it refers to can have its properties mutated, so `const` is not an immutable value.

JavaScript also has the ability to `freeze()` objects, but those objects are only frozen at the root level, meaning that a nested object can still have mutated properties.

## Libraries

* [seamless-immutable](https://github.com/rtfeldman/seamless-immutable)
* [mori](https://github.com/swannodette/mori)
* [Immutable.js](https://facebook.github.io/immutable-js/)
* [Elsa - A babel plugin for replacing object and array literals with immutable versions](https://github.com/JonAbrams/elsa)

## Ways to Mutate

You need to also be mindful of:

* Time
* Random numbers
* Logging

```js
handleProductUpVote(productId) {
  // While map() create a new array, the element inside
  // is references the original
  const nextProducts = this.state.products.map((product) => {
    if (product.id === productId) {
      // Since the element still references the original
      // we need to clone it...
      return Object.assign({}, product, {
        votes: product.votes + 1,
      });
    } else {
      return product;
    }
  });
    this.setState({    products: nextProducts,  });}
```

### Array

* [Array's mutator methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#Mutator_methods)

```js
// To add a new item, instead of push(), we'd use concat()
items.concat(newItem)

// Or the slow performance spread method
[...items, newItem]

// Or use Immutable.js List
const items = List([1, 2, 3])
const items1 = items.push(3, 4, 5)

// Put item in front
const items = this.state.items.slice()
item.unshift('first item')

// To remove an item, instead of splice(), we'd use a simple filter()
items.filter((s, _idx) => idx !== _idx)
```

### Object

```js
// ES6
Object.assign({}, originalObject, { field: newValue })

// ES7 Object spread
{...originalObject, field: newValue}
```

## Immutable.js

