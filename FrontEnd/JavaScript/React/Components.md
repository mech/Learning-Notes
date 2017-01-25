# Components

* [React FAQ](https://github.com/timarney/react-faq)
* [React A-ha Moments](https://tylermcginnis.com/react-aha-moments/)

## Forms

* [react-reform](https://github.com/codecks-io/react-reform)

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

These are 2 **BAD** ways to do binding in component, because it will cause Component to re-render as different reference has been passed every time:

* `<Component onClick={() => this.handleClick()} />`
* `<Component onClick={this.handleClick.bind(this)} />`

We need to pre-bind them in the constructor.

## State

* [Thinking statefully](https://daveceddia.com/thinking-statefully/)
* [A visual guide to state in React](https://daveceddia.com/visual-guide-to-state-in-react/)

State is only reserved for interactivity, that is, data changes over time.

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

### Use function in `setState`

See [for more details](https://medium.com/@shopsifter/using-a-function-in-setstate-instead-of-an-object-1f5cfd6e55d1#.u0tfkb84b)

```js
// Recommended if you need to set state based on previous state
this.setState((prevState, props) => {
  return {
    showForm: !prevState.showForm
  }
})
```

The 2nd argument to `setState` to a callback function which will be invoked when `setState` has finished and the component is re-rendered. It's best to use other lifecycle method rather than relying on this callback function.

## Lifecycle Methods

## shouldComponentUpdate

* [Turbocharge Your React Application with shouldComponentUpdate and Immutable.js](https://blog.javascripting.com/2015/03/31/turbocharge-your-react-application-with-shouldcomponentupdate-and-immutable-js/)

React's `render()` do not really ask the DOM to immediately render itself. Instead `render()` is just a method that return a virtual DOM. If you tell React that certain component and their children need not be invoked with the `render()` through `shouldComponentUpdate`, then React will skip those calls.

> Let's say you have a list composed of many components with a complicated nested structure, and one item in the list changes. It would be a waste of resources to perform a diff on every single component in the list. By implementing `shouldComponentUpdate`, you can basically tell React to ignore all the components except the one that changed.

The default behavior of `shouldComponentUpdate` is to let React do a virtual DOM diff to arrive at a decision whether to update or not which can be time consuming.

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

## Higher Order Components

Behavioral-Oriented Component. HOC encapsulate behavior and typically does not render anything. It enhance and compose component.

* [HOC: A React Application Design Pattern from SitePoint](https://www.sitepoint.com/react-higher-order-components/)

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

## Keys

* [Why having proper key is important](http://buildwithreact.com/article/in-depth-diffing)

## Blogs

* [Dave Ceddia](https://daveceddia.com/)
* [Tyler McGinnis](https://tylermcginnis.com/)
* [Mark Erikson](http://blog.isquaredsoftware.com/)
