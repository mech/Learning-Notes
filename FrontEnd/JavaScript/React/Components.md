# Components

> React allows us to describe and break up our view into components.

* Self-sufficient, do one thing good
* Easy to integrate with

> Learning functional programming completely changed my design process. There's a lot of parallels you can directly apply to your work day to day — it's about composition and I think this is something super useful for the design system we're working on. Rather than starting with a layout or a big marketing page and breaking it down, I love the idea of starting with the smallest possible primitives and building up and up and up.

* [Pure UI Control](https://medium.com/@asolove/pure-ui-control-ac8d1be97a8d)
* [Single Responsibility Components](https://www.youtube.com/watch?v=pSdp92Up8O8)
* [**Under the hood: ReactJS**](https://bogdan-lyashenko.github.io/Under-the-hood-ReactJS/)
* [React Architecture and Best Practices](https://github.com/markerikson/react-redux-links/blob/master/react-architecture.md)
* [React FAQ](https://github.com/timarney/react-faq)
* [React FAQ Site](https://reactfaq.site/)
* [Airbnb React/JSX Style Guide](https://github.com/airbnb/javascript/tree/master/react)
* [React Patterns](https://github.com/chantastic/reactpatterns.com)
* [React Bits - React patterns, techniques, tips and tricks](https://github.com/vasanthk/react-bits)
* [React A-ha Moments](https://tylermcginnis.com/react-aha-moments/)
* [Exploration: Front-end JavaScript at Artsy in 2017](https://artsy.github.io/blog/2017/02/05/Front-end-JavaScript-at-Artsy-2017/)
* [10 React Mini Patterns](https://hackernoon.com/10-react-mini-patterns-c1da92f068c5#.7ev5n4sus)
* [A deep dive into children in React](https://mxstbr.blog/2017/02/react-children-deepdive/)
* [Components in Figma](https://medium.com/figma-design/components-in-figma-e7e80fcf6fd2#.c40b1b20h)
* [Our Best Practices for Writing React Components](https://engineering.musefind.com/our-best-practices-for-writing-react-components-dec3eb5c3fc8#.ktdv8jlh2)
* [Functional React — Get your App outta my Component](https://medium.com/@adamterlson/functional-react-series-part-1-get-your-app-outta-my-component-92656ae13e25?ref=mybridge.co)
* [Embracing stateless functional component](https://medium.com/javascript-inside/embracing-functions-in-react-d7d558d8bd30)
* [Examples app to build](https://medium.freecodecamp.org/every-time-you-build-a-to-do-list-app-a-puppy-dies-505b54637a5d)
* [React Behavioral Wrapper Components](https://medium.com/@fastphrase/react-behavioral-wrapper-components-97b87a0108e8)
* [All the Conditional Renderings in React](https://www.robinwieruch.de/conditional-rendering-react/)

---

1. Static components (HTML).
2. Determine where state should live. Data flow down.
3. Inverse data flow up. Propagating events from child to parent.
4. Go to top-level container component to communicate with data server.

> There are a lot of similarities in the way we build UIs with React and the principles of FP, and the more we are aware of it, the better our code will be - `UI = f(state)`

## The Rise of Component, Mythical Man-Month and Atomic Design

* React enable isolated components
* Based on Atomic Design principles
* Allow distributed work similar to picking cotton
* 2013, Brad Frost published Atomic Design
* 2013, Facebook released React

## Security

* [The Most Common XSS Vulnerability in React.js Applications](https://medium.com/node-security/the-most-common-xss-vulnerability-in-react-js-applications-2bdffbcc1fa0)

## ReactElement vs ReactComponent

* ReactElement is stateless and immutable. It is basically a plain JavaScript object.
* ReactComponent has a render() that is expected to return ReactElement.

## React 16

```js
const Aux = (props) => {
  // Before React 16
  return <div>{props.children}</div>

  // After React 16
  // Good for flexbox, grid, tables
  return props.children
}
```

## Examples and Case Studies

* [real-world-react-apps](https://github.com/jeromedalbert/real-world-react-apps)
* [Some good touch and animation examples](https://medium.com/@sanchitgn/what-ive-learnt-developing-a-modern-progressive-web-app-d3abe69933fa)

## Fiber

* [A look inside Fiber](http://makersden.io/blog/look-inside-fiber/)

## Frameworks

* [rakt](https://github.com/threepointone/rakt)
* [next.js](https://github.com/zeit/next.js/)
* [ARc (Atomic React)](https://github.com/diegohaz/arc)
* [rekit](https://github.com/supnate/rekit)
* [formidable-react-starter](https://github.com/FormidableLabs/formidable-react-starter)
* [OkCupid file structure](https://tech.okcupid.com/how-okcupid-organizes-its-multi-page-react-app/)
* [quantum-blox](https://github.com/metaphorical/quantum-blox)

---

* [Universal create-react-app, step by step](https://medium.com/leanjs/universal-create-react-app-step-by-step-b80ba68d125d)

## Storybook

* [Using React within a Design System](https://medium.com/buildit/using-react-within-a-design-system-73d4bb0cc822)

## Tips

* [Tips to learn React and Redux](https://www.robinwieruch.de/tips-to-learn-react-redux/)

1. Use Recompose before implement your own HOC
2. Lift state up or down before using Redux
3. Don't initialize states using props
4. Store things in state that your are going to render()
5. State changes over time. So let's eliminate time. Let's be declarative and beat the passage of time.
6. Look at jQuery for widget options/props
7. Use Compound Components to compose just like `<option>` inside `<select>`
8. Keep the props that your component expects to a minimum and make sure you use them individually. Do not just blindly spread the props as you may cause unnecessary re-renders.
9. **Never let them know your next move.** Keep your components generic enough that they solve only one view element, really well. If your components are small and flexible, then they will not be pigeonhole’d and able to be composed into larger units.
10. Your `render()` method should be as lightweight and fast as possible.

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

* [Building a React Component Library - Part 1](https://hackernoon.com/building-a-react-component-library-part-1-d8a1e248fe6c)
* Reusable components shouldn't worry about where data is coming from. It should come from the parent as `props`.
* Reusable should deal with its interaction however and not rely on parent.
* Small components with clean interface

## Composition Patterns

* Props
* Container and Presentational
* HOC with **explicit props**
* Recompose
* Function as Child
* Compound Component with **implicit props**

## Props

Be careful when passing props as `null`. Any default prop value will not be used if the props is `null`.

> What existed as mutable state is passed down as immutable props.

* props are immutable
* Use `componentWillReceiveProps` to re-render if props changes

## States

> Visualizing all the discrete states an application can be in will make your design systems better.

* [Thinking statefully](https://daveceddia.com/thinking-statefully/)
* [A visual guide to state in React](https://daveceddia.com/visual-guide-to-state-in-react/)
* [`setState()` Gate - Navigating React `setState()` Behavior Confusion](https://medium.com/javascript-scene/setstate-gate-abc10a9b2d82#.66ktn17qa)
* [Functional `setState` is the future of React](https://medium.freecodecamp.com/functional-setstate-is-the-future-of-react-374f30401b6b#.2b7ljzb5c)
* [5 types of application states](http://jamesknelson.com/5-types-react-application-state/)
* As much as possible, treat state also as immutable, same as props

State is only reserved for interactivity, that is, data changes over time.

Every time we can compute (derivables) the final value from the props, we should not store any data into the state.

```js
// We receive currency and value from props
// And we always show them together
this.state = {
  price: `${props.currency}${props.value}`
}

// We may think that it would be better to store it in the state
// and use the value inside the render()
render() {
  return <div>{this.state.price}</div>
}

// Problem is when the props change, the UI won't re-render
// because the constructor is called once only!
// Instead we should create a helper/getter function
getPrice() {
  return `${this.props.currency}${this.props.value}`
}
```

### Eliminate Time

**Eliminate time** as much as possible. If your `render()` accumulate state over time, you will want to eliminate that. See how Ryan Florence [remove time](https://www.youtube.com/watch?v=kp-NOggyz54).

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

```js
function shouldIKeepSomethingInReactState() {
  if (canICalculateFromPros()) {
    // Don't duplicate date from props in state
    // Calculate what you can in render() method
    return false
  }
  
  if (!amIUsingItInRenderMethod()) {
    // Don't keep something in the state if you don't use it
    // for rendering.
    // For example, API subscriptions are better off as custom
    // private fields or variables in external modules.
    return false
  }
  
  // You can use React state for this!
  return true
}
```

### Use function in `setState`

* [When to use callback function in setState](https://medium.com/@voonminghann/when-to-use-callback-function-of-setstate-in-react-37fff67e5a6c)

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

Remember that functional `setState` is async, so can't reference outdated events from within the closure:

```js
// Problematic
handleChange(event) {
  this.setState(() => ({
    searchTerm: event.target.value
  }))
}

// Solution
handleChange(event) {
  const value = event.target.value
  this.setState(() => ({
    searchTerm: value
  }))
}
```

Remember to use Higher Order Function if you extract your functional setState outside of your component:

```js
setSearchResult(result) {
  const { hits, page } = result
  this.setState(updateResult(hits, page))
}

// Somewhere outside the component
// This function return a function that match functional setState's signature
const updateResult = (hit, page) => (prevState, props) => {
}
```

### Do not initialize state using props

The `constructor` is only called once when the component is created. If you initialize state using props and later change the props values, the component will never use that value.

> If you read through articles on React, you may see that "setting state from props is an 'anti-pattern'". The main issue is handling updates to the state in response to the props changing. This can be a valid concern but should be understood as advice, not the ultimate rule.

Especially for initializing form data, sometimes this rule can be broken.

```js
<Form initialData={data}>
</Form>
```

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

> In React, immutable structures often lead to better performance: when data changes in a mutable representation, **you'll likely need to rely on React's virtual DOM** to determine whether components should update; alternatively, in an immutable representation, you can use a basic strict equality check to determine whether an update should occur.

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

* [How to safely use React context](https://medium.com/@mweststrate/how-to-safely-use-react-context-b7e343eff076)

| Parent/Grandparent                                                    | Child                                            |
|-----------------------------------------------------------------------|--------------------------------------------------|
| `childContextTypes` - defines what context to supply                  | `contextTypes` - defines what context to consume |
| `getChildContext()` - keys are merged on to context (last merge wins) | `this.context`                                   |

```js
class Provider extends Component {
  // Here, we promise to provide these context
  static childContextTypes = {
    store: PropTypes.object.isRequired
  }

  // This is a lifecycle hook
  // Whenever a child request for context, this will be called
  getChildContext() {
    return {
      store: this.props.store
    }
  }
  
  render() {
    return this.props.children
  }
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

The components above leaf components are primarily concerned with orchestration.

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

* [**Downshift - Compound Component and Function as Child example**](https://medium.com/@kentcdodds/introducing-downshift-for-react-b1de3fca0817)
* [return-null](https://github.com/joshwcomeau/return-null)
* [Function as child components](https://medium.com/merrickchristensen/function-as-child-components-5f3920a9ace9)
* [ReactCasts #2 - Function as Child Components](https://www.youtube.com/watch?v=WE3XAt9P8Ek)

**Alert!** You lose the ability to optimize your component at the render().

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

class Log extends PureComponent {
  render() {
    console.info(this.props.children)
    return null; // so nothing is rendered to the DOM
  }
}

// Use it
<Log>{currentUser}</Log>

<Speak message={this.state.message} />
```

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

* Called **Member Expressions** like `<TabBarIOS.Item>`

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
* [ReactCasts](https://www.youtube.com/channel/UCZkjWyyLvzWeoVWEpRemrDQ/videos)

## Books

* [React Design Patterns and Best Practices (DONE)](https://www.safaribooksonline.com/library/view/react-design-patterns/9781786464538/)
* [Learning React](https://www.safaribooksonline.com/library/view/learning-react-1st/9781491954614/ch02.html)
* Fullstack React (DONE)
* The Missing Form Handbook of React (DONE)
* [Advanced React.js (DONE)](https://app.pluralsight.com/library/courses/reactjs-advanced/table-of-contents)