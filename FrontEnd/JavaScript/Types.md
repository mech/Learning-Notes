# Type Checking

* [Type systems will make you a better JavaScript programmer](http://jaredforsyth.com/type-systems-js-dev/#/)

```
▶ npm install -g flow-bin
▶ npm install -g flow-typed

▶ npm install --save-dev babel-plugin-transform-flow-strip-types

// Create .flowconfig file
▶ flow init
```

```js
// You wouldn't want to write such checking code
function greet(greeting, months, age) {
  if (arguments.length !== 3)
    throw new Error('must be called with 3 arguments')
  if (typeof greeting !== 'string')
    throw new Error('greeting must be a string')
  if (!Array.isArray(months))
    throw new Error('months must be an array')
  if (typeof age !== 'number')
    throw new Error('age must be a number')
}

// Much better with Flow
function greet(greeting: string,
               months: Array<string>,
               age: number) {
}
```

* If it is hard to type check, it is probably hard to understand

```js
function isValid(items: Array<string>): boolean {
}
```

## Type-First Approach

```js
type Post {
  title: string,
  createdAt: Date,
  contents: string,
  authors: Array<{
    name: string,
    location: string,
    numberOfPosts: number
  }>
}
```