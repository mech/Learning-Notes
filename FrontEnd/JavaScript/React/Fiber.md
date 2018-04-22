# React 16 - Fiber

> So much of React's architecture is based on stuff game developers figured out decades ago. - https://twitter.com/acdlite/status/978696799757086720

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
* Fiber is just a JavaScript object representing the Virtual Stack Frame of an React component. Just like VDOM is a JavaScript object representing a component's DOM.
* Time slicing or async setState (make use of functional setState instead of plain object - see `ReactDOM.unstable_deferredUpdates`)
* Uses `requestIdleCallback` to cooperate with the browser's overall work schedule
* Improve startup time rendering components as they become available to the browser without the need to wait for a whole bundle to be downloaded.

## Async Rendering

* [Update on Async Rendering](https://reactjs.org/blog/2018/03/27/update-on-async-rendering.html)
* [Example of main thread blocking](https://build-mbfootjxoo.now.sh/)
* [Issue on how react-redux is going to interact with "Suspense" and "Time-Slicing" behavior](https://github.com/reactjs/react-redux/issues/890)
* [A Walkthrough of *that* React Suspense Demo](https://dev.to/swyx/a-walkthrough-of-that-react-suspense-demo--4j6a)


## Error Boundaries

## Return Multiple Elements

