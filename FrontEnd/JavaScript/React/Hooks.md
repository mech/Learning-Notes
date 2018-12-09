# Hooks

* [Fullstack React: An Introduction to Hooks in React](https://www.fullstackreact.com/articles/an-introduction-to-hooks-in-react/)
* [Why React Hooks, and how did we even get here?](https://medium.freecodecamp.org/why-react-hooks-and-how-did-we-even-get-here-aa5ed5dc96af)
* [How to convert withRouter to a React Hook](https://itnext.io/how-to-convert-withrouter-to-a-react-hook-f7babe0be79b)
* [useNavbar](https://frontarm.com/demoboard/?id=6bafab26-0391-48ae-80ff-38dbf8cefafa)
* [Making Sense of React Hooks](https://medium.com/@dan_abramov/making-sense-of-react-hooks-fdbde8803889)

Reusing logic still suck in React.

The main building block in React is Component and there are 2 ways of sharing behaviors/code so far:

* Higher-order components
* Render props

Wrapper hell. Lifecycle issues in huge components. Understanding classes is also confusing. Binding and `this` present its own set of problem.

We need a simpler, lightweight component that do not use ES6 class.

> React doesn't provide a **stateful primitive** simpler than a class component.

## useState

Stateful class component can have state, but functional pure component can only depend on passed in props to update their state. useState changes that!

## useContext

No only read the context for you but also subscribe automatically for you and re-render when the context changes.

Flat is always better than nested wrapper hell.

## useEffect

* Lifecycle methods
* Firing off API request
* Use for imperative DOM mutation, interfacing with browser API

Run both after the initial render and on every update. May have performance issues (if for example you are subscribing to event like resize event).