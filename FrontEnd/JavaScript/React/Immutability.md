# Immutability

Ideally we want `shouldComponentUpdate` to always return `false`, but that is not realistic. So the next best option is to do simple and fast equality check.

Equality check for value like string, boolean and integer is simple. Equality check for objects, arrays and functions is problematic.

Immutable.js allows us to detect changes in JavaScript objects/arrays without resorting to the inefficiencies of deep equality checks, which in turn allows React to avoid expensive re-render operations when they are not required.

* [React, Redux and Immutable.js: Ingredients for Efficient Web Applications](https://www.toptal.com/react/react-redux-and-immutablejs)
* [updeep - Easily update nested frozen objects and arrays in a declarative and immutable manner](https://github.com/substantial/updeep)

A `const` object can't be reassigned to refer to a completely different object, but the object it refers to can have its properties mutated, so `const` is not an immutable value.

JavaScript also has the ability to `freeze()` objects, but those objects are only frozen at the root level, meaning that a nested object can still have mutated properties.

## Ways to Mutate

### Array

```js
items.concat(newItem)

[...items, newItem]
```

### Object

```js
// ES6
Object.assign({}, originalObject, { field: newValue })

// ES7 Object spread
{...originalObject, field: newValue}
```