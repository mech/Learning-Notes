# React 16 - Fiber

* https://twitter.com/dan_abramov/status/977298210816393216
* https://twitter.com/acdlite/status/978412930973687808

Many names:

* Async mode
* Concurrent mode
* Time slicing

> So much of React's architecture is based on stuff game developers figured out decades ago. - https://twitter.com/acdlite/status/978696799757086720

* [The Rise of JavaScript Scheduling](https://www.loxodrome.io/post/javascript-scheduling/)
* [Scheduling in React - Philipp Spiess](https://philippspiess.com/scheduling-in-react/)
* [#7942 - Fiber Principles: Contributing To Fiber](https://github.com/facebook/react/issues/7942)
* [What's New in React 16 and Fiber Explanation](https://medium.com/@treyhuffine/react-16-features-and-fiber-explanation-e779544bb1b7)
* [A look inside Fiber](http://makersden.io/blog/look-inside-fiber/)
* [What is React Fiber?](https://giamir.com/what-is-react-fiber)
* [React Fiber resources](https://github.com/koba04/react-fiber-resources)
* [Didact Fiber: Incremental reconciliation](https://engineering.hexacta.com/didact-fiber-incremental-reconciliation-b2fe028dcaec)

---

* Rewrite of React core algorithm for reconciliation
* The main thread is the same as the UI thread. Only the main thread can change the DOM.
* Solve choppy frame rates and laggy input.
* Assign different priorities to different types of updates.
* Fiber is just a JavaScript object representing the Virtual Stack Frame of a React component. Just like VDOM is a JavaScript object representing a component's DOM.
* Time slicing or async setState (make use of functional setState instead of plain object - see `ReactDOM.unstable_deferredUpdates`)
* Uses `requestIdleCallback` to cooperate with the browser's overall work schedule
* Improve startup time rendering components as they become available to the browser without the need to wait for a whole bundle to be downloaded.

With the help of the new Fiber architecture rewrite React can now pause during rendering and yield to the main thread for prioritized tasks like updating input element UI.

## Concurrent Mode and Async Rendering

In Concurrent Mode, `render()` could be invoked multiple times without actually committing (like applying changes to the DOM).

In Strict Mode, `render()` is rendered twice to simulate the behavior Concurrent Mode will be having in the future in order for you to easily catch any bug during development mode.

* [Update on Async Rendering](https://reactjs.org/blog/2018/03/27/update-on-async-rendering.html)
* [Example of main thread blocking](https://build-mbfootjxoo.now.sh/)
* [Issue on how react-redux is going to interact with "Suspense" and "Time-Slicing" behavior](https://github.com/reactjs/react-redux/issues/890)
* [A Walkthrough of *that* React Suspense Demo](https://dev.to/swyx/a-walkthrough-of-that-react-suspense-demo--4j6a)

## Code Splitting with React Lazy

* [How to retry when React lazy fails](https://goenning.net/2018/11/16/how-to-retry-dynamic-import-with-react-lazy/)

## Error Boundaries

* [Handling Errors in JavaScript: The Definitive Guide](https://levelup.gitconnected.com/the-definite-guide-to-handling-errors-gracefully-in-javascript-58424d9c60e6)

## Return Multiple Elements

## Time-Slicing

* React doesn't block the thread while rendering
* Feels synchronous if device is fast
* Feels responsive if device is slow
* Only final rendered state is displayed
* Make sure your most important renders are rendered first like text entry

## Suspense

* Pause state update until data is ready
* On fast network, render after the whole tree is ready
* On slow network, precisely control the loading states
* Simplify data fetching, code splitting and any kind of async data requirement
* [React Suspense with the Fetch API](https://medium.com/swlh/react-suspense-with-the-fetch-api-cc655aced759)