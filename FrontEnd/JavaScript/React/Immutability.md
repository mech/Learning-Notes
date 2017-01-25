# Immutability

Ideally we want `shouldComponentUpdate` to always return `false`, but that is not realistic. So the next best option is to do simple and fast equality check.

Equality check for value like string, boolean and integer is simple. Equality check for objects, arrays and functions is problematic.

Immutable.js allows us to detect changes in JavaScript objects/arrays without resorting to the inefficiencies of deep equality checks, which in turn allows React to avoid expensive re-render operations when they are not required.

* [React, Redux and Immutable.js: Ingredients for Efficient Web Applications](https://www.toptal.com/react/react-redux-and-immutablejs)
* [updeep - Easily update nested frozen objects and arrays in a declarative and immutable manner](https://github.com/substantial/updeep)

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