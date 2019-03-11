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

> Classes may seem like the ideal thing to hold state since that's what they're designed for. However, React is more written like a declarative function that keeps getting executed over and over to simulate it being reactive. Those two things have an impedance mismatch and that keeps leaking when we think of these as classes.
> 
> Another issue is just that the conceptual mental model for React is just functions calling other functions recursively. There is a lot of value to express it in those terms to help build the correct mental model.

* Currently in class component, it is very hard to share stateful logics.
* Lifecycle tracking is too hard
* Artificial hierarchy due to render props being structured in a fixed tree-like manner
* [GDG Salt Lake DevFest 2018: Why React Hooks](https://www.youtube.com/watch?v=zWsZcBiwgVE)

```js
// Creating a Media Listener component
class Media extends Component {
  state = {
    matches: window.matchMedia(this.props.query).matches
  }
  
  componentDidMount() {
    this.setup()
  }
  
  setup() {
    let media = window.matchMedia(this.props.query)
    if (media.matches !== this.state.matches) {
      this.setState({ matches: media.matches })
    }
    
    let listener = () => this.setState({ matches: media.matches })
    media.addListener(listener)
    this.removeListener = () => media.removeListener(listener)
  }
  
  componentDidUpdate(prevProps) {
    if (prevProps.query !== this.props.query) {
      this.removeListener()
      this.setup()
    }
  }
  
  componentWillUnmount() {
    this.removeListener()
  }
  
  render() {
    return this.props.children(this.state.matches)
  }
}

function App() {
  return (
    <Media query="(max-width: 400px)">
      {small => (
        <p>
          Small? {small ? "Yep" : "Nope"}
        </p>
      )}
    </Media>
  )
}
```

Let's do it in the hooks way

```js
function useMedia(query) {
  let [matches, setMatches] = useState(
    window.matchMedia(query).matches
  )
  
  // cDM, cDU
  useEffect(() => {
    let media = window.matchMedia(query)
    if (media.matches !== matches) {
      setMatches(media.matches)
    }
    let listener = () => setMatches(media.matches)
    media.addListener(listener)
    
    return () => media.removeListener(listener)
  }, [query])
}

function App() {
  let small = useMedia("(max-width: 400px)")
  
  return (
    <p>
      Small? {small ? "Yep" : "Nope"}
    </p>
  )
}
```

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

Hooks are billed as the new way to share logic. But do not confuse this with sharing common state with other components in the tree. For that you still need the React Context API. Hooks are local shareable isolated logic, whilst context is more for shareable global state.

No only read the context for you but also subscribe automatically for you and re-render when the context changes.

Flat is always better than nested wrapper hell.

```js
const FormContext = React.createContext();

function App() {
  const [state, dispatch] = useReducer(appReducer, []);
  
  return (
    <FormContext.Provider value={dispatch}>
      <MyChildrenThatUseDispatcher items={state} />
    </FormContext.Provider>
  )
}

function MyChildrenThatUseDispatcher {
  const dispatch = useContext(FormContext);
  
  return (
    <button onClick={() => dispatch({ type: 'DELETE', payload: id })}>Delete</button>
  )
}
```

## useEffect

Where you do imperative thing in a declarative world.

Essentially combination of `componentDidMount`, `componentDidUpdate` and `componentWillUnMount`.

* Lifecycle methods
* Firing off API request
* Use for imperative DOM mutation, interfacing with browser API

Run both after the initial render and on every update. May have performance issues (if for example you are subscribing to event like resize event).

You interact with third party libraries in useEffect. You also do HTTP call in useEffect until we have Suspense.

Due to batching and concurrent mode, the closed over values (closure) are actually not reactive. They capture the state as it was.

## useReducer

The general pattern of dispatching and then centralizing the logic to transition between states at a higher level seems to be having great success. It also solves many quirks with callbacks in React, leads to many more intuitive solutions around complex state transitions. Especially in a concurrent world.

So I see useReducer as the central API more so than useState. useState is still nice since it's very concise for simple use cases and easy to explain, but people should probably look into useReducer or similar patterns early on.

* [An example of using `useReducer`](https://medium.com/@diegoalmesp/not-another-reactjs-hooks-post-823f2d5d6ba4)
* [Are React Hooks Slower than Class Components?](https://www.youtube.com/watch?v=tKRWuVOEB2w)

When dealing with form, we can use `useReducer` to not render any form that does not need to be rendered when certain state changes.

You can also use `useReducer` when you are sick of having to deal with so many individual `useState` and just want to dump all things into a single state object.

Another interesting reason to use `useReducer` is you can pass down the `dispatch` function into your children via props or context.

## useMemo

## useCallback

## useImperativeMethods

## Libraries and Tools

* [retoggle](https://github.com/Raathigesh/retoggle)

## Videos

* [Let's HOOK up with React](https://www.youtube.com/watch?v=h9qHKDlsnP0)
* [React Hooks: A Complete Introduction](https://www.youtube.com/watch?v=jd8R0a2Ur8Q)
* [Introducing React Hooks](https://www.youtube.com/watch?v=mxK8b99iJTg)
* [React Hooks: Advanced Hooks](https://www.youtube.com/watch?v=YKmiLcXiMMo)