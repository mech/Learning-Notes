# Components

* [React FAQ](https://github.com/timarney/react-faq)
* [React FAQ Site](https://reactfaq.site/)
* [Airbnb React/JSX Style Guide](https://github.com/airbnb/javascript/tree/master/react)
* [React Patterns](https://github.com/chantastic/reactpatterns.com)
* [React A-ha Moments](https://tylermcginnis.com/react-aha-moments/)
* [Exploration: Front-end JavaScript at Artsy in 2017](https://artsy.github.io/blog/2017/02/05/Front-end-JavaScript-at-Artsy-2017/)
* [10 React Mini Patterns](https://hackernoon.com/10-react-mini-patterns-c1da92f068c5#.7ev5n4sus)
* [A deep dive into children in React](https://mxstbr.blog/2017/02/react-children-deepdive/)
* [Components in Figma](https://medium.com/figma-design/components-in-figma-e7e80fcf6fd2#.c40b1b20h)
* [Our Best Practices for Writing React Components](https://engineering.musefind.com/our-best-practices-for-writing-react-components-dec3eb5c3fc8#.ktdv8jlh2)
* [Functional React — Get your App outta my Component](https://medium.com/@adamterlson/functional-react-series-part-1-get-your-app-outta-my-component-92656ae13e25?ref=mybridge.co)
* [Embracing stateless functional component](https://medium.com/javascript-inside/embracing-functions-in-react-d7d558d8bd30)

## Tips

* [Tips to learn React and Redux](https://www.robinwieruch.de/tips-to-learn-react-redux/)

1. Use Recompose before implement your own HOC
2. Lift state up or down before using Redux
3. 

## Verbs for component name

You can use verb to describe a component:

```js
const App = () => (
  <div>
    <Grid />
    <SetSize />
  </div>
)
```

## Reusable Components

* Reusable components shouldn't worry about where data is coming from. It should come from the parent as `props`.
* Reusable should deal with its interaction however and not rely on parent.

## Forms

* [Form Validation as HOC](https://medium.com/javascript-inside/form-validation-as-a-higher-order-component-pt-1-83ac8fd6c1f0#.fv2zg6miy)
* [react-reform](https://github.com/codecks-io/react-reform)
* [react-jsonschema-form](https://github.com/mozilla-services/react-jsonschema-form)
* [Web Form Validation: Best Practices](https://www.smashingmagazine.com/2009/07/web-form-validation-best-practices-and-tutorials/)
* [How to create a Redux-Form with validation and initialized values](https://www.davidmeents.com/blog/create-redux-form-validation-initialized-values/)

```js
// Generic change handler
handleChange({ target }) {
  this.setState({
    [target.name]: target.value
  })
}
```

```js
const AddTodo = ({onAddClick}) => {
  let input
  
  return (
    <div>
      <input ref={node => input = node} />
      <button onClick={() => {
        onAddClick(input.value)
        input.value = ''
      }}>
        Add Todo
      </button>
    </div>
  )
}
```

What API is good for inputs:

```js
<Form onSubmit={this.handleSubmit}>
  <Text name="email" label="Email" isRequired isEmail />
  <Password name="password" label="Password" isRequired />
</Form>
```

## Handling Events

* [Best alternative to binding in render()](https://daveceddia.com/react-best-alternative-bind-render/)
* [React Binding Patterns: 5 Approaches for Handling `this`](https://medium.com/@housecor/react-binding-patterns-5-approaches-for-handling-this-92c651b5af56?ref=mybridge.co)
* [Event Switch](https://github.com/chantastic/reactpatterns.com#event-switch)

Synthetic Events are reusable and there is a single global handler. This means you cannot store a synthetic event and reuse it later because it becomes `null` right after the action. If you really want to store it, you can use `persist()`.

```js
// SyntheticEvent is pooled and reuse and will be reset, so this won't work
handleClick(evt) {
  setTimeout(function() {
    // ERROR - name will be null
    console.log(evt.target.name)
  }, 1000)
}
```

```js
// Note that this returns a function
select(choice) {
  return (evt) => {
    this.setState({
      payMethod: choice
    })
  }
}

// Note our onClick is calling a function first that return a function
// This is common pattern for passing arguments to handlers.
// We close over the choice argument when we call `select`.
render() {
  return (
    <PayPalPaymentChoice
      onClick={this.select('PayPal')}
    />
  )
}
```

```js
// `todos` and `onTodoClick` are promoted to the props because we
// want this to be a presentational component
// BAD - poor performance as it need to re-render whenever props
// changes due to function binding and lack of shouldComponentUpdate
const TodoList = ({
  todos,
  onTodoClick
}) => (
  <ul>
    {todos.map(todo =>
      <Todo
        key={todo.id}
        {...todo}
        onClick={() => onTodoClick(todo.id)}
      />
    )}
  </ul>
)

// At the top-level App
<TodoList
  todos={visibleTodos}
  onTodoClick={id =>
    store.dispatch({
      type: 'TOGGLE_TODO',
      id
    })
  }
/>
```

```js
// Notice that the remove() is passed in as well as id
const Item = ({ id, title, remove }) => (
  <div className="item">
    {title}
    <span
      className="deleteItem"
      onClick={() => remove(id)}
    >Delete</span>
  </div>
)
```

These are 2 **BAD** ways to do binding in component, because it will cause Component to re-render as different reference has been passed every time:

* `<Component onClick={() => this.handleClick()} />`
* `<Component onClick={this.handleClick.bind(this)} />`

We need to pre-bind them in the constructor.

## Refs

* [When to use Ref on a DOM node in React](https://www.robinwieruch.de/react-ref-attribute-dom-node/)

In case we need it, React gives us access to the actual DOM nodes in a way that we can perform imperative operations with them (like 3rd-party libraries).

Using refs is imperative (i.e. `input.focus()`) and we should avoid using refs as much as possible because they force the code to be more imperative and harder to read and maintain.

It is important to note that when setting the ref callback on a non-native component, the reference will be the whole instance itself and not the DOM node:

```js
<Input ref={element => this.element = element} />
```

## Props

Be careful when passing props as `null`. Any default prop value will not be used if the props is `null`.

## States

* [Thinking statefully](https://daveceddia.com/thinking-statefully/)
* [A visual guide to state in React](https://daveceddia.com/visual-guide-to-state-in-react/)
* [`setState()` Gate - Navigating React `setState()` Behavior Confusion](https://medium.com/javascript-scene/setstate-gate-abc10a9b2d82#.66ktn17qa)
* [Functional `setState` is the future of React](https://medium.freecodecamp.com/functional-setstate-is-the-future-of-react-374f30401b6b#.2b7ljzb5c)
* [5 types of application states](http://jamesknelson.com/5-types-react-application-state/)

State is only reserved for interactivity, that is, data changes over time.

Every time we can compute (derivables) the final value from the props, we should not store any data into the state.

Eliminate time as much as possible. If your `render()` accumulate state over time, you will want to eliminate that. See how Ryan Florence [remove time](https://www.youtube.com/watch?v=kp-NOggyz54).

Declaring state let you eliminate time.

Don't clash imperative programming with declarative/stateful thinking.

```js
// Can you render sound?
<Tone
  isPlaying={this.state.isPlaying}
  pitch={this.state.pitch}
  volume={this.state.volume}
/>
```

```js
class FetchUser extends Component {
  state = { user: null }

  componentDidMount() {
    fetch(url).then(res => res.json()).then(user => {
      this.setState({ user })
    })
  }  

  render() {
    return this.props.children(this.state)
  }
}

<FetchUser>
{() => <div />}
</FetchUser>
```

Every time the state changes React runs the `render()` again unless told by `shouldComponentUpdate()` not to. Or else it's default behavior is to re-render every single time.

### Use function in `setState`

See [for more details](https://medium.com/@shopsifter/using-a-function-in-setstate-instead-of-an-object-1f5cfd6e55d1#.u0tfkb84b)

```js
// Recommended if you need to set state based on previous state
this.setState((prevState, props) => {
  return {
    showForm: !prevState.showForm
  }
})

// Notice the parentheses if there is not `return`
this.setState(prevState => ({ expanded: !prevState.expanded }))
```

The 2nd argument to `setState` to a callback function which will be invoked when `setState` has finished and the component is re-rendered. It's best to use other lifecycle method rather than relying on this callback function.

## PropTypes

We should always try to pass primitive props to components because they are simpler to validate and to compare. However, in some case it is unavoidable to pass objects and in those cases, we should declare our `propTypes` using **shapes**.

```js
const Profile = ({ user }) => (
  <div>{user.name} {user.surname}</div>
)

Profile.propTypes = {
  user: React.PropTypes.shape({
    name: React.PropTypes.string.isRequired,
    surname: React.PropTypes.string
  }).isRequired
}
```

**Custom PropType**

```js
const age = (props, propName) => {
  if (!(props[propName] > 0 && props[propName] < 100>)) {
    return new Error(`${propName} must be between 1 and 99`)
  }
  return null
}
```

## Lifecycle Methods

### componentWillMount

* Called before `render()`
* Called only once
* No access to DOM
* A chance to handle configuration (like global events), update state since props and states are defined
* `setState()` will not trigger a re-render, but you can still use it to prepare

### componentDidMount

* Called only once, so won't have infinite loop if you use `setState()`
* By walking backwards, we know that every child has mounted and also run its own `componentDidMount()`. This guarantees the parent can access the Native UI elements for itself and its children. The leaf components always start first.

### componentWillReceiveProps

Because props are immutable, the parent must provide the new values when there is changes.

If component needs to derive state from props then you need to process those props in both the constructor and `componentWillReceiveProps` especially when the component is going to be receiving new properties from its ancestors.

* Calling `setState()` will not trigger re-render
* Ignored by `forceUpdate()`

### shouldComponentUpdate

* [Turbocharge Your React Application with shouldComponentUpdate and Immutable.js](https://blog.javascripting.com/2015/03/31/turbocharge-your-react-application-with-shouldcomponentupdate-and-immutable-js/)
* Ignored by `forceUpdate()`

React's `render()` do not really ask the DOM to immediately render itself. Instead `render()` is just a method that return a virtual DOM. If you tell React that certain component and their children need not be invoked with the `render()` through `shouldComponentUpdate`, then React will skip those calls.

> Let's say you have a list composed of many components with a complicated nested structure, and one item in the list changes. It would be a waste of resources to perform a diff on every single component in the list. By implementing `shouldComponentUpdate`, you can basically tell React to ignore all the components except the one that changed.

The default behavior of `shouldComponentUpdate` is to let React do a virtual DOM diff to arrive at a decision whether to update or not which can be time consuming.

If `shouldComponentUpdate` returns `false`, the component and all its children's `render` methods are not called during an update of its parents.

### componentWillUpdate

* Will be called whenever we decide to `render()`
* Sort of like `componentWillMount`, but not quite
* You can access `refs` but is not recommended since it will be soon be out of date, but using it for animation may be helpful if just temporarily.
* Calling `setState()` will result in infinite loop

### componentDidUpdate

* Sort of like `componentDidMount`
* Have access to DOM, refs, etc.
* Good when you want to update 3rd party library
* Avoid `setState()`

```js
// Access our chart instance and update it when data has changed
componentDidUpdate(prevProps, prevState) {
  if (prevProps.data !== this.props.data) {
    this.chart = c3.load({
      data: this.props.data
    })
  }
}
```

## Context

| Parent/Grandparent                                                    | Child                                            |
|-----------------------------------------------------------------------|--------------------------------------------------|
| `childContextTypes` - defines what context to supply                  | `contextTypes` - defines what context to consume |
| `getChildContext()` - keys are merged on to context (last merge wins) | `this.context`                                   |

```js
class Provider extends Component {
  getChildContext() {
    return {
      store: this.props.store
    }
  }
  
  render() {
    return this.props.children
  }
}

Provider.childContextTypes = {
  store: React.PropTypes.object
}
```

User of `Provider` will need to:

```js
const AddTodo = (props, { store }) => {
}

// Opt to receive context
AddTodo.contextTypes = {
  store: React.PropTypes.object
}
```

**More examples**

```js
// SFC take props, context as arguments
// Not reusable as it needs a parent (<Provider/>??) with the
// currency as child context types to work
const Price = ({ value }, { currency }) => (
  <div>{currency}{value}</div>
)

Price.propTypes = {
  value: React.PropTypes.number
}

Price.contextTypes = {
  currency: React.PropTypes.string
}

// We can use Recompose's getContext() to create a HOC
// that can receive the context and pass it as props
const Price = ({ currency, value }) => (
  <div>{currency}{value}</div>
)

// getContext is a HOC using partial application to
// specialize itself
const withCurrency = getContext({
  currency: React.PropTypes.string
})

const PriceWithCurrency = withCurrency(Price)
```

## Container and Presentational Pattern

React components typically contain a mix of **logic** and **presentation**.

By logic, it can be:

* API calls
* Data manipulation
* Event handling

There is no rules that say that the Presentational component must not have a state. For example, it could keep a UI state inside it like toggling menu etc.

You data team can work on container component and your designer can work on iterating the UI. The data team can even replace the presentational component with another one just for debugging purposes.

Being able to work in parallel on the same component is a big win for teams, especially for those companies where building interfaces is an iterative process.

Applying this pattern without real reason can make the codebase less useful. So we need to think carefully before we refactor into this pattern.

## Children

Always use `React.Children.map` instead of `props.children.map` because we cannot assume that `children` will be an array. It could be a single object.

```js
// Single object
<Parent>
  <h1>Welcome</h1>
</Parent>

// Array
<Parent>
  <h1>Welcome</h1>
  <h2>props.children will now be an array</h2>
</Parent>
```

This is because when a component has a single child, React optimizes the creation of the elements and avoid allocating an array for performance reasons.

```js
Button.propTypes = {
  children: React.PropTypes.oneOfType([
    React.PropTypes.array,
    React.PropTypes.element
  ])
}
```

### Function as Child (vs HOC)

* [Function as child components](https://medium.com/merrickchristensen/function-as-child-components-5f3920a9ace9)

```js
<Fetch url="...">
  {data => <List data={data} />}
</Fetch>

<Ratio>
  {(width, height, hasComputed) => (
    hasComputed && height > TOO_TALL
      ? <TallThing />
      : <NotSoTallThing />
  )}
</Ratio>

```

## Higher Order Components

A type of Container Component.

Components by itself are great to achieve reusability and composability. But what if different components in different domains share the same behavior? Early React gives use mixins to share behaviors.

```js
// Pre-React 0.13
// Creating mixins is very similar to creating a component
const WindowResize = {
  getInitialState() {
    return {
      innerWidth: window.innerWidth
    }
  }
  
  componentDidMount() {
    window.addEventListener('resize', this.handleResize)
  }
  
  componentWillUnmount() {
    window.removeEventListener('resize', this.handleResize)
  }
  
  handleResize() {
    this.setState({
      innerWidth: window.innerWidth
    })
  }
}

// Switching that into HOC
const withInnerWidth = Component => (
  class extends React.Component {
    constructor(props) {
      super(props)
      
      this.state = {
        innerWidth: window.innerWidth
      }
      
      this.handleResize = this.handleResize.bind(this)
    }
    
    componentDidMount() {
      window.addEventListener('resize', this.handleResize)
    }
  
    componentWillUnmount() {
      window.removeEventListener('resize', this.handleResize)
    }

    handleResize() {
      this.setState({
        innerWidth: window.innerWidth
      })
    }
    
    render() {
      return <Component {...this.props} {...this.state} />
    }
  }
)

// Wrapped component
const MyComponent = ({ innerWidth }) => {
  console.log('window.innerWidth', innerWidth)
}

// Enhanced component
const MyComponentWithInnerWidth = withInnerWidth(MyComponent)
```

Mixins tend to communicate with the component using the state, while HOC communicate using props which is much more nicer.

The advantages of HOC over mixins: we do not pollute state and we do not require the component to implement any function.

Behavioral-Oriented Component. HOC encapsulate behavior and typically does not render anything. It enhance and compose component.

Good for addressing cross-cutting concerns or common functionalities, such as logging and tracking and listening for window resize events.

* [HOC: A React Application Design Pattern from SitePoint](https://www.sitepoint.com/react-higher-order-components/)
* [Functions as child components and HOC](http://rea.tech/functions-as-child-components-and-higher-order-components/)
* [Real World Examples of Higher-Order Components](http://rea.tech/reactjs-real-world-examples-of-higher-order-components/)
* [Abstract your UI from elemental component (`<input>`), then use HOC to add additional functionalities](https://www.youtube.com/watch?v=5rtbSYl70ak)
* [Why The Hipsters Recompose Everything](https://medium.com/javascript-inside/why-the-hipsters-recompose-everything-23ac08748198#.qbwgfntlp)

Benefits of HOC:

* Do things before and/or after it calls that component
* Avoid rendering the component if certain criteria is not met
* Update the props passed to that component, or add new props
* Transform the output of rendering a component (e.g. wrap with extra DOM elements, etc.)
* Enforce Single Responsibility Principle. Authenticated HOC should only be concerned with authentication and route handler component should be concerned with route handling only.

It's rare to need to build a HOC; typically most components you build will directly render nodes to the DOM. Building a HOC that's abstract enough to reuse take planning. It's often easier to write a HOC after you see recurring patterns within your components.

```js
// HOCs are function that take a component as input and return an enhanced one as output
const HOC = Component => EnhancedComponent
```

```js
// Simple HOC
export default function(ComposedComponent) {
  class Authentication extends Component {
    render() {
      return <ComposedComponent {...props} />
    }
  }
  
  return Authentication
}

// If we remove the first and last line, you'll have no problem seeing
// that it is just a normal component that import ComposedComponent
```

Using Redux for authenticated component:

```js
export default function(ComposedComponent) {
  class Authentication extends Component {
    componentWillMount() {
      if (!this.props.authenticated) {
        <Redirect to="/" />
      }
    }
    
    componentWillUpdate(nextProps) {
      if (!nextProps.authenticated) {
        <Redirect to="/" />
      }
    }
    
    render() {
      return <ComposedComponent {...props} />
    }
  }
  
  function mapStateToProp(state) {
    return { authenticated: state.auth.authenticated }
  }
  
  return connect(mapStateToProp)(Authentication)
}
```

```js
const withPlayQueue = (component) => class PlayQueue extends React.Component {
  state = {
    isPlaying: false,
    playQueue: [],
    currentTrack: -1
  }
  
  addTrack = (track) => this.setState({
    playQueue: this.state.playQueue.concat(track)
  })
  
  render() {
    const playQueue = {
      addTrack: this.addTrack
    }
    
    return (
      <View>
        <Player />
        <Component playQueue={playQueue} {...this.props} />
      </View>
    )
  }
}

const App = () => { ... }
module.exports = withPlayQueue(App)
```

```js
const showHide = (Title, Content) => class ShowHide extends React.Component {
  constructor(props) {
    super(props)
    this.state = { isActive: false }
    this.onToggle = this.onToggle.bind(this)
  }
  
  render() {
    return (
      <div>
        <Title onClick={this.onToggle} />
        { this.state.isActive && <Content /> }
      </div>
    )
  }
  
  onToggle() {
    this.setState({ isActive: !this.state.isActive })
  }
}

const Title = props => <p {...props}>title<p>
const Content = props => <p>content<p>

const ConcreteToggle = showHide(Title, Content)
```

**Tracking metric HOC example**

The trackingData were specific to every page, but the tracking calls were not.

```js
import tracker from './tracking-api'

const metricTracking = ComposedComponent => React.createClass({
  componentDidMount() {
    tracker.trackPageLoad(this.props.trackingData)
  },
  
  componentDidUpdate() {
    tracker.trackPageLoad(this.props.trackingData)
  },
  
  render() {
    return <ComposedComponent {...this.props} />
  }
})
```

**Some more examples**

```js
// We are returning a stateless functional component
const withClassName = Component => props => (
  <Component {...props} className="my-class" />
)
```

### HOC with partial application

* [Curry or Partial Application?](https://medium.com/javascript-scene/curry-or-partial-application-8150044c78b8#.fxhqqauo2)

You can use partial application to let your HOC receives parameters first before applying it.

```js
const HOC = args => Component => EnhancedComponent
```

See the [Recompose](https://github.com/acdlite/recompose) library fore more examples.

```js
const enhanced = compose(
  flattenProp('user),
  renameProp('username', 'name'),
  withInnerWidth
)
```

**Warning:** Don't abuse HOC. Every time you wrap a component into a HOC, you are adding a new `render()`, a new lifecycle method call, and memory allocation. It may be a performance issues.

## Keys

* [Why having proper key is important](http://buildwithreact.com/article/in-depth-diffing)
* [Issues with numeric keys vs string?](https://discuss.reactjs.org/t/performance-problems-with-react-when-using-a-big-list/3432/13)

## Data Fetching

* Two unconnected sibling can share data through their common Parent
* You can create a generic HOC to fetch data from any API endpoints

React enforces a very interesting pattern to make data go from the root to the leaves. This pattern is called **Unidirectional Data Flow**.

Children can hold local state and use it as props for its nested component. Re-rendering of that local state only affect the nested component downward.

There are 2 lifecycle hooks where we can fetch data:

* `componentWillMount` - fired before `render()`
* `componentDidMount` - fired after `render()`

Using `componentWillMount` seems to be the right choice because we want to load the data as soon as we can, but there is a caveat: `componentWillMount` is fired on both server and client-side rendering. Naturally firing an async API call on the server can give you unexpected result.

We can use HOC to load data on behalf of the enhanced component and it would provide the data to the child in the form of props.

```js
// A generic HOC for fetching simple data
// Use partial application to pass in the URL
const withData = url => Component => class extends React.Component {
  constructor(props) {
    super(props)
    this.state = { data:[] }
  }
  
  componentDidMount() {
    const endpoint = typeof url === 'function'
      ? url(this.props)
      : url
      
    fetch(endpoint)
      .then(res => res.json())
      .then(data => this.setState({ data }))
  }
  
  render() {
    return <Component {...this.props} {...this.state} />
  }
}

// Use it
const List = ({ data: gists }) => (
  <ul>
    {gists.map(gist => (
      <li key={gist.id}>{gist.description}</li>
    ))}
    <li>
  </ul>
)

const ListWithGists = withData(props => `https://github.com/${props.username}/gists`)(List)

// Pass the props along
<ListWithGists username="mech" />
```

## Passthrough Props

You wrote the `<Component>`, your consumer want to pass `props` to the underlying element without any hinder.

* [Building a property passthrough (can't be used with Flow)](http://jamesknelson.com/building-a-property-passthrough-higher-order-component-for-react/)

```js
const { theme, className, children, ...others } = this.props;
const classes = `NavBar NavBar-${theme} ${className}`
return <div {...others} className={classes}>{children}</div>
```

## Namespaced Components

```js
import Toolbar from './Toolbar'

render() {
  <Toolbar.Item label="News" />
  <Toolbar.Menu label="News" />
}

// At the Toolbar.jsx
export Item
export Menu
```

## Layouts

* Slots and Fills - https://github.com/camwest/react-slot-fill
* Portals - https://github.com/tajo/react-portal
* Modals

## Blogs

* [Dave Ceddia](https://daveceddia.com/)
* [Tyler McGinnis](https://tylermcginnis.com/)
* [Mark Erikson](http://blog.isquaredsoftware.com/)
* [Guillermo Rauch](https://rauchg.com/essays)
* [Jack Hsu](https://jaysoo.ca/)

## Videos

* [React Component Patterns by Michael Chan](https://www.youtube.com/watch?v=YaZg8wg39QQ)