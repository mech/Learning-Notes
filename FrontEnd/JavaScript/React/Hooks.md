# Hooks

> Hardest things about hooks so far has been figuring out good patterns whilst tripping over bad ones. (Like dispatching inside a useEffect without passing an empty array as a second argument), infinite loops are not cool, people. - ‪@erik_hellman‬

* [RFC: React Hooks](https://github.com/reactjs/rfcs/pull/68)
* [Making setInterval Declarative with React Hooks](https://overreacted.io/making-setinterval-declarative-with-react-hooks/)
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

## Why Hooks

* Currently in class component, it is very hard to share stateful logics.
* Lifecycle tracking is too hard
* Artificial hierarchy due to render props being structured in a fixed tree-like manner
* [GDG Salt Lake DevFest 2018: Why React Hooks](https://www.youtube.com/watch?v=zWsZcBiwgVE)

## useState

Stateful class component can have state, but functional pure component can only depend on passed in props to update their state. useState changes that!

Allow you to manage only 1 value, be it single primitive or object. It differs from regular React class component's state where you typically manages many values in one shot.

It is much simpler and does not do any merging of state.

```js
function CalendarPicker({ numOfCalendar }) {
  const [numOfCalendar, setNumOfCalendar] = useState(numOfCalendar)
  
  return (
    <>
      {Array(numOfCalendar).fill().map(() => {
        <Calendar />
      })}
    </>
  )
}
```

Each useState hook is totally separate and should not share state. If you want to share state, please use Context.

`useState` is also a very good way to view your slice of state in a much more cleaner and clearer way. Think about this as the Reduce slice of state, only this time each `useState` control their own slice of data.

To just set state once you can pass function instead of a value:

```js
// Notice that it is a function that run once only
const [name, setName] = useState(() => {
  window.localStorage.getItem('geo-chat:name')
})
```

## useContext

No only read the context for you but also subscribe automatically for you and re-render when the context changes.

Flat is always better than nested wrapper hell.

## useEffect

Essentially combination of `componentDidMount`, `componentDidUpdate` and `componentWillUnMount`.

* Lifecycle methods
* Firing off API request
* Use for imperative DOM mutation, interfacing with browser API

Run both after the initial render and on every update. May have performance issues (if for example you are subscribing to event like resize event).

You interact with third party libraries in useEffect. You also do HTTP call in useEffect until we have Suspense.

## useReducer

* [An example of using `useReducer`](https://medium.com/@diegoalmesp/not-another-reactjs-hooks-post-823f2d5d6ba4)

## Libraries and Tools

* [retoggle](https://github.com/Raathigesh/retoggle)

## Videos

* [Let's HOOK up with React](https://www.youtube.com/watch?v=h9qHKDlsnP0)
* [React Hooks: A Complete Introduction](https://www.youtube.com/watch?v=jd8R0a2Ur8Q)
* [Introducing React Hooks](https://www.youtube.com/watch?v=mxK8b99iJTg)