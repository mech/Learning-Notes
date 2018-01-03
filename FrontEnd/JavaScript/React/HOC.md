# Higher Order Components - Behavior rather than Markup

Container components are not very reusable when it comes to rendering different results. Take for example this container component:

```js
class MyContainer extends React.Component {
  state = { loading: true }
  
  componentDidMount() {
    fetch(url).then().then()
  }
  
  render() {
    return <FixedStaticView {...this.state} />
  }
}
```

We can see that `<FixedStaticView>` is somehow fixed and known ahead of time. You can't reuse the data fetching logic with different views. This is where HOC comes in or even more recently Render Props.

Higher order function return a function that is usually enhanced with some special behaviors.

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

* [**React Higher Order Components in depth**](https://medium.com/@franleplant/react-higher-order-components-in-depth-cf9032ee6c3e)
* [Single-Prop HOCs – Better Composition in React](https://www.okgrow.com/posts/compose-react-sphoc)
* [Facebook official HOC doc](https://facebook.github.io/react/docs/higher-order-components.html)
* [HOC: A React Application Design Pattern from SitePoint](https://www.sitepoint.com/react-higher-order-components/)
* [Functions as child components and HOC](http://rea.tech/functions-as-child-components-and-higher-order-components/)
* [Real World Examples of Higher-Order Components](http://rea.tech/reactjs-real-world-examples-of-higher-order-components/)
* [Abstract your UI from elemental component (`<input>`), then use HOC to add additional functionalities](https://www.youtube.com/watch?v=5rtbSYl70ak)
* [Why The Hipsters Recompose Everything](https://medium.com/javascript-inside/why-the-hipsters-recompose-everything-23ac08748198#.qbwgfntlp)
* [Higher Order Components: Theory and Practice](http://engineering.blogfoster.com/higher-order-components-theory-and-practice/)
* [Reusable State with Higher Order Components](https://daveceddia.com/extract-state-with-higher-order-components/)
* [Functional Approach to Higher Order Components and Recompose](https://codebrahma.com/functional-approach-higher-order-components-recompose/)
* [Understanding Higher Order Components](https://medium.freecodecamp.org/understanding-higher-order-components-6ce359d761b)
* [react-only-if](https://github.com/MicheleBertoli/react-only-if)
* [HOC and render props pattern](https://lucasmreis.github.io/blog/simple-react-patterns/)
* [I'm Breaking up with Higher Order Components](https://medium.com/tandemly/im-breaking-up-with-higher-order-components-44b0df2db052)

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

// Partial application
const HOC = args => Component => EnhancedComponent
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

**Loading example**

```js
// Do not pass isLoading property to inner Component
const withLoading = (Component) => ({ isLoading, ...rest }) =>
  props.isLoading ? <Loading /> : <Component ...rest />
  
// Usage
const ContentWithLoading = withLoading(Content)

<ContentWithLoading isLoading={true} />
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

**withData**

```js
const withData = url => Component => (
  class extends React.Component {
    constructor(props) {
      super(props)
      this.state = { data: [] }
    }
    
    componentDidMount() {
      const endpoint = typeof url === 'function'
        ? url(this.props) // where the dynamic username is at
        : url
        
      fetch(endpoint)
        .then(res => res.json())
        .then(data => this.setState({ data }))
    }
    
    render() {
      return <Component {...this.props} {...this.state} />
    }
  }
)

const withGists = withDate(
  props => `https://api.github.com/users/${props.username}/gists`
)

const ListWithGists = withGists(List)

// We want to pass in a dynamic username
<ListWithGists username="gaearon" />
```

### HOC with Ramda's compose or [Recompose](https://github.com/acdlite/recompose)

```js
import { compose } from 'ramda'
// import { compose } from 'lodash/fp'
// import { compose } from 'recompose'
// import { compose } from 'react-apollo'

const VisibleTodoList = compose(
  withRouter,
  connect(mapStateToProps, mapDispatchToProps)
)(TodoList)

// It can get more and more
const enhance = compose(
  withRouter,
  withState('searchTerm', 'setSearchTerm'),
  connect(mapStateToProps, mapDispatchToProps),
  graphql(RepositoryQuery, {
    options: ({ match }) => ({
      variables: {
        owner: match.params.owner,
        name: match.params.name
      }
    })
  })
)

export default enhance(Repository)
```

```js
// One way to write the compose()
const compose = (...fns) =>
  (arg) =>
    fns.reduce(
      (composed, f) => f(composed),
      arg
    )
```

`compose()` takes in multiple functions as arguments and returns a single function. The returned function expects one argument `arg`. When this function is invoked, the `fns` array is piped starting with the argument we want to send through the function. The `arg` becomes the initial value for `composed` and then each iteration of the reduced callback returns. `composed` is the result of the previous function output. Eventually, the last function will be invoked and the last result returned.

This is just a simple example of `compose()` and does not handle more than one argument or deal with arguments that are not functions. Other implementations of `compose()` may use `reduceRight` which would compose the functions in reverse order.

```js
// 4 HOC to decorate Todos dumb component
compose(myTodos, createTodo, deleteTodo, isAdmin)(Todos)
```

**A Store Provider example**

```js
// At <App>, we pass in store
class App extends Component {
  static childContextTypes = {
    store: PropTypes.object
  }
  
  getChildContext() {
    return {
      store: this.props.store
    }
  }
  
  state = this.props.store.getState()
}

// HOC that give children interested in store their store
const storeProvider = Component => {
  const WithStore = (props, { store }) =>
    <Component {...props} store={store} />
    
  WithStore.contextTypes = {
    store: PropTypes.object
  }
  
  WithStore.displayName = `${Component.name}Container`
  
  return WithStore
}

// Or if you want state
const storeProvider = Component => {
  return class extends React.Component {
    static displayName = `${Component.name}Container`
    static contextTypes = {
      store: PropTypes.object
    }

    render() {
      return <Component {...this.props} store={this.context.store} />
    }
  }
}
```

## Static and Hoisting

* [hoist-non-react-statics](https://github.com/mridgway/hoist-non-react-statics)

## Performance Issues

Don't abuse HOC. Every time you wrap a component into a HOC, you are adding a new `render()`, a new lifecycle method call, and memory allocation. It may be a performance issues.