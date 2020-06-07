# Hooks

> Hardest things about hooks so far has been figuring out good patterns whilst tripping over bad ones. (Like dispatching inside a useEffect without passing an empty array as a second argument), infinite loops are not cool, people. - ‪@erik_hellman‬

* [Cross-cutting functionality in React using HOC, Render Props and Hooks](https://pawelgrzybek.com/cross-cutting-functionality-in-react-using-higher-order-components-render-props-and-hooks/)
* [**Very good demonstration of hooks with isMounted, isIO**](https://itnext.io/essential-react-hooks-design-patterns-a04309cc0404)
* [React Hook Flow Diagram](https://www.bram.us/2019/03/11/react-hook-flow-diagram/)
* [Everything you need to know about React Hooks](https://medium.com/@vcarl/everything-you-need-to-know-about-react-hooks-8f680dfd4349)
* [How to migrate from Recompose to React Hooks](https://medium.com/stationfive/how-to-migrate-from-recompose-to-react-hooks-89b2981c03d)
* [Support both Hooks and Render Props with One Simple Trick](https://americanexpress.io/hydra/)
* [RFC: React Hooks](https://github.com/reactjs/rfcs/pull/68)
* [Making setInterval Declarative with React Hooks](https://overreacted.io/making-setinterval-declarative-with-react-hooks/)
* [Fullstack React: An Introduction to Hooks in React](https://www.fullstackreact.com/articles/an-introduction-to-hooks-in-react/)
* [Why React Hooks, and how did we even get here?](https://medium.freecodecamp.org/why-react-hooks-and-how-did-we-even-get-here-aa5ed5dc96af)
* [How to convert withRouter to a React Hook](https://itnext.io/how-to-convert-withrouter-to-a-react-hook-f7babe0be79b)
* [useNavbar](https://frontarm.com/demoboard/?id=6bafab26-0391-48ae-80ff-38dbf8cefafa)
* [Making Sense of React Hooks](https://medium.com/@dan_abramov/making-sense-of-react-hooks-fdbde8803889)
* [Simple Code Reuse with React Hooks](https://blog.bitsrc.io/simple-code-reuse-with-react-hooks-432f390696bf)

Reusing logic still suck in React.

The main building block in React is Component and there are 2 ways of sharing behaviors/code so far:

* Higher-order components
* Render props

Wrapper hell. Lifecycle issues in huge components. Understanding classes is also confusing. Binding and `this` present its own set of problem.

We need a simpler, lightweight component that do not use ES6 class.

> React doesn't provide a **stateful primitive** simpler than a class component.

## Lifecycle

**First forget about React lifecycle on mounting and un-mounting and think about hooks in synchronisation/scheduling concept.**

Think of hook as state synchronisation and effect synchronisation.

> The question is not "when does this effect run", the question is "with which state does this effect synchronise with"
> useEffect(fn) // all state
> useEffect(fn, []) // no state
> useEffect(fn, [these, states])

## Trying to set state after component has unmounted

* [React state update on an unmounted component](https://www.debuggr.io/react-update-unmounted-component/)

## Examples

* [How to Build a Todo List with React Hooks](https://medium.freecodecamp.org/how-to-build-a-todo-list-with-react-hooks-ebaa4e3db3b)
* [Class features vs. Hooks equivalents](https://medium.com/soluto-engineering/react-class-features-vs-hooks-equivalents-745368dafdb3)

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

## Rules of Hooks

* [Why Do React Hooks Rely on Call Order?](https://overreacted.io/why-do-hooks-rely-on-call-order/)

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

To just set state once you can pass function instead of a value. This is so that whenever your functional component render, the useState will not keep on constructing and re-initialising.

```js
// Notice that it is a function that run once only, on the first render!
const [name, setName] = useState(() => {
  window.localStorage.getItem('geo-chat:name')
})
```

**Immutability and useState**

useState does not do merging for you, it is a shallow update only, you typically have to handle immutability yourself (or it won't re-render)

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

**What to put in context**

Anything. You can put function, you can put hooks, you can put heavy object, you can put anything!

## useRef

* [6 Practical Applications for useRef](https://medium.com/frontend-digest/6-practical-applications-for-useref-2f5414f4ac68)

Besides letting us to control DOM element directly. `useRef` can also be used as a generic container whose current property is mutable and can hold any value. Think of it like `this.instanceVariable`.

It also be used to capture previous state or props.

```js
const numRef = useRef(0)
numRef.current++
```

```js
const el = useRef()

return (
  <textarea ref={el}></textarea>
)
```

```js
const Timer = (props) => {
  const intervalRef = useRef()
  
  useEffect(() => {
    const id = setInterval()
    intervalRef.current = id
    
    return () => {
      clearInterval(intervalRef.current)
    }
  })
}
```

## useEffect

Without the 2nd parameter, `useEffect()` will always keep running between render which is a good default because your application will not feel broken.

Call **after render**. React will remember the function you passed and will call it **after the DOM updates**.

Where you do imperative thing in a declarative world.

Essentially combination of `componentDidMount`, `componentDidUpdate` and `componentWillUnMount`.

* Lifecycle methods
* Firing off API request
* Use for imperative DOM mutation, interfacing with browser API

Run both after the initial render and on every update. May have performance issues (if for example you are subscribing to event like resize event).

You interact with third party libraries in useEffect. You also do HTTP call in useEffect until we have Suspense.

Due to batching and concurrent mode, the closed over values (closure) are actually not reactive. They capture the state as it was.

## useReducer

> Should I use multiple useState or useReducer?
> 
> For independent things (isHovering and textInput), multiple useState.
> 
> For things that change together (isFetching and fetchedItems), or if their next state depends on previous (todos), I prefer useReducer. - https://twitter.com/dan_abramov/status/1083330668522864640

The general pattern of dispatching and then centralizing the logic to transition between states at a higher level seems to be having great success. It also solves many quirks with callbacks in React, leads to many more intuitive solutions around complex state transitions. Especially in a concurrent world.

So I see useReducer as the central API more so than useState. useState is still nice since it's very concise for simple use cases and easy to explain, but people should probably look into useReducer or similar patterns early on.

* [useReducer is more capable](https://levelup.gitconnected.com/interesting-points-from-abramovs-a-complete-guide-to-useeffect-99ef9e136a19)
* [**From Redux to Hooks**](https://staleclosures.dev/from-redux-to-hooks-case-study/)
* [Replacing redux with react hooks and context - Part 1](https://medium.com/octopus-labs-london/replacing-redux-with-react-hooks-and-context-part-1-11b72ffdb533)
* [The React Hooks based alternative to Redux and the Flux pattern](https://medium.com/capbase-engineering/part-3-the-react-hooks-based-alternative-to-redux-and-the-flux-pattern-a726220a8a9a)
* [An example of using `useReducer`](https://medium.com/@diegoalmesp/not-another-reactjs-hooks-post-823f2d5d6ba4)
* [Are React Hooks Slower than Class Components?](https://www.youtube.com/watch?v=tKRWuVOEB2w)

When dealing with form, we can use `useReducer` to not render any form that does not need to be rendered when certain state changes.

You can also use `useReducer` when you are sick of having to deal with so many individual `useState` and just want to dump all things into a single state object.

Another interesting reason to use `useReducer` is you can pass down the `dispatch` function into your children via props or context.

## useMemo

* [Some example of useMemo() and memo()](https://github.com/facebook/react/issues/15156#issuecomment-474590693)

## useCallback

Don't use this all the time. Measure first.

* [**When to useMemo and useCallback**](https://kentcdodds.com/blog/usememo-and-usecallback)

## useLayoutEffect

## useImperativeMethods

For library author mostly.

## Render Props

* [Render props is still useful for inversion of control thing](https://kentcdodds.com/blog/react-hooks-whats-going-to-happen-to-render-props)
* [With Suspense and Hooks, do Render Props still have a place?](https://www.youtube.com/watch?v=_jehVItn7Vo)

## Form with Hooks

* [**React Hook Form**](https://react-hook-form.com/)
* [React Hooks - Custom Hooks (form validation hook)](https://www.youtube.com/watch?v=tmlzjnZy6ZQ)

```js
const useInput = (initial) => {
  const [value, setValue] = useState(initial)
  return {
    value, 
    onChange: e => setValue(e.target.value)
  }
}

// Use it
const Form = () => {
  const email = useInput('')
  const password = useInput('')
  
  return (
    <div>
      <input type="email" {...email} />
      <input type="password" {...password} />
    </div>
  )
}
```

## Libraries and Tools

* [retoggle](https://github.com/Raathigesh/retoggle)

## Videos

* [Let's HOOK up with React](https://www.youtube.com/watch?v=h9qHKDlsnP0)
* [React Hooks: A Complete Introduction](https://www.youtube.com/watch?v=jd8R0a2Ur8Q)
* [Introducing React Hooks](https://www.youtube.com/watch?v=mxK8b99iJTg)
* [React Hooks: Advanced Hooks](https://www.youtube.com/watch?v=YKmiLcXiMMo)
* [Fun with React Hooks - Michael Jackson and Ryan Florence](https://www.youtube.com/watch?v=1jWS7cCuUXw)
* [How React Hooks Change The Way We Build Forms](https://www.youtube.com/watch?v=8yo44xN7-nQ)
* [Apollo + React Hooks + TypeScript = 🥰 by: James Reggio, Web Platform Lead, Convoy](https://www.youtube.com/watch?v=IxmrRiA9Gso)