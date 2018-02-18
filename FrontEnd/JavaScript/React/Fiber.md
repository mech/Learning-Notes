# React 16 - Fiber

* [What's New in React 16 and Fiber Explanation](https://medium.com/@treyhuffine/react-16-features-and-fiber-explanation-e779544bb1b7)
* [A look inside Fiber](http://makersden.io/blog/look-inside-fiber/)
* [What is React Fiber?](https://giamir.com/what-is-react-fiber)
* [React Fiber resources](https://github.com/koba04/react-fiber-resources)

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

* [Example of main thread blocking](https://build-mbfootjxoo.now.sh/)


## Error Boundaries

## Return Multiple Elements

