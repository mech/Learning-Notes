# Async

* [Async version of React really works](https://twitter.com/jlongster/status/1054554506736910336)
* [How JavaScript works: Event loop and the rise of Async programming + 5 ways to better coding with async/await](https://blog.sessionstack.com/how-javascript-works-event-loop-and-the-rise-of-async-programming-5-ways-to-better-coding-with-2f077c4438b5)
* [Handling errors with async/await and promises](https://medium.com/@vcarl/handling-errors-with-async-await-and-promises-cd2fea534f08)

Async is basically eliminating callback hell.

## Books

* [Mastering Async/Await](http://asyncawait.net/jsweekly)

## Promises

* [Passing data between Promise callbacks](http://2ality.com/2017/08/promise-callback-data-flow.html)
* [JavaScript's Promise Leaks Memory](https://alexn.org/blog/2017/10/11/javascript-promise-leaks-memory.html)
* [p-cancelable - Create a promise that can be canceled](https://github.com/sindresorhus/p-cancelable)
* [Cancelling Requests with Abortable Fetch](https://www.loxodrome.io/post/cancelling-requests/)

Before you dive into the wonderful world of async/await, it's important that you understand and appreciate Promises.

* Guaranteed future - Good and bad. Can't be cancelled, this means you're executing code you probably don't want to. Can't do auto-complete well. Route loading also problematic.
* Immutable
* Single value - problematic in modern web app
* Caching
* Can't do try-catch error handling
* Still really using callback, but just nicely using thenables

```js
// Promise.prototype.finally()
db.open()
.then()
.then()
.catch()
.finally()
```

## Async/Await

> I also see a surprising amount of code that uses async/await mixed with classic callbacks or promise chains. While passing an async function to a promise's then() function as shown below is valid, it misses the point of async/await:

```js
// Works, but misses the point
getCustomer().then(async function(customer) {
  const order = await getOrders(customer.id);
  
  return { customer, order };
});

// Do this instead
const customer = await getCustomer();
const order = await getOrders(customer.id);
return { customer, order };
```

* [Common Async/Await Design Patterns in Node.js](http://thecodebarbarian.com/common-async-await-design-patterns-in-node.js.html)
* [Using ES2017 Async Functions](https://css-tricks.com/using-es2017-async-functions/)
* [Node.js Async Function Best Practices](https://nemethgergely.com/async-function-best-practices/)
* [JavaScript async/await: The Good Part, Pitfalls and How to Use](https://hackernoon.com/javascript-async-await-the-good-part-pitfalls-and-how-to-use-9b759ca21cda)
* [Understanding JavaScript's async await](https://ponyfoo.com/articles/understanding-javascript-async-await)
* `await` takes in any Promises
* Use normal try-catch to handle exceptions
* Built on Promises and Generators
* **An async function will always itself return a promise**
* When we await, it pauses the function, not the entire code
* Is non-blocking, so other asynchronous function can still run while we are waiting 

```js
// This return a Promise<any>
const fetchGitHubUser = async (handle) => {
  const url = `https://api.github.com/users/${handle}`
  const response = await.fetch(url)
  return await response.json()
}

// An IIFE
(async () => {
  const user = await fetchGitHubUser('mech')
  console.log(user.name)
})();

// Using Promise.all
async function showUserAndRepos(handle) {
  const [user, repos] = await Promise.all([
    fetchFromGitHub(`/users/${handle}`),
    fetchFromGitHub(`/users/${handle}/repos`)
  ])
}

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

## React

To use Async/Await on lifecycle methods, you need `babel-polyfill`.

```js
entry: [
  'babel-polyfill',
  './index.jsx'
]

class App extends React.Component {
  state = {
    answer: 42
  }

  asyncFunc = () => {
    return Promise.resolve(37)
  }
  
  async componentDidMount() {
    this.setState({
      answer: await this.asyncFunc()
    })
  }
}
```

## Semaphore

* [semaphorejs](https://github.com/nybblr/semaphorejs)

## Web Worker

* [greenlet - Move an async function into its own thread](https://github.com/developit/greenlet)
* [Parallel programming in JavaScript](https://itnext.io/achieving-parallelism-in-javascript-using-web-workers-8f921f2d26db)
* Can only pass messages

## Videos

* [Async patterns to scale your multicore JavaScript elegantly](https://www.youtube.com/watch?v=726eZyVtC0Y)

