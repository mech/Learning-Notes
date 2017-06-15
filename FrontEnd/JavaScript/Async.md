# Async

## Promises

* Guaranteed future - Good and bad. Can't be cancelled, this means you're executing code you probably don't want to. Can't do auto-complete well. Route loading also problematic.
* Immutable
* Single value - problematic in modern web app
* Caching

## Generator

Utilize generators to write better asynchronous code, by yielding promises instead of chaining them with `then()`, creating a more readable control flow.

```js
function * getUser(username) {
  const res = yield fetch(`https://api.github.com/users/${username}`)
  const json = yield res.json()
  return json
}
```

The async/await feature brings this approach to a new level. This control flow can be implemented without the need of a third party library. Instead of generator functions we use `async` functions, and instead of `yield` we use the `await` keyword.

```js
async function getUser(username) {
  const res = await fetch(`https://api.github.com/users/${username}`)
  const json = await res.json()
  return json
}
```

## RxJS

* [Netflix JavaScript Talks - RxJS + Redux + React = Amazing!](https://www.youtube.com/watch?v=AslncyG8whg)