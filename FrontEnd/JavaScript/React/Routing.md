# Routing

* [RR4 docs](https://react-router.now.sh/)
* [Simple declarative Redux state with React Router 4 server side rendering](https://medium.com/@AlexFaunt/satisfying-your-apps-state-343118b0730d#.gh5ihu9ii)

```
Route Component === Route Handler === Screen Container === Controller (Horror)
```

You can think of URL as being an external keeper of state. URL is also a state.

Starting from v4, routes are just components. The components now define the composition of the UI. Before all your routes may be in `index.js`:

```js
ReactDOM.render(
  <Provider store={store}>
    <Router history={browserHistory}>
      <Route path="/" component={HomeContainer} />
      <Route path="/r/:name" component={SubredditContainer} />
    </Router>
  </Provider>
)
```

In v4, you need to replace your `props.children` (outlets) with several matches/screens that you intend to have:

```js
const App = (props) => {
  <BrowserRouter>
    <div class="container">
      <Route exact path="/" component={HomeContainer} />
      <Route exact path="/r/:name" component={SubredditContainer} />
      <Route path="/one" render={() => <h2>One</h2>} />
      <Route path="/re" render={() => (<Redirect to="/10/20" />)} />
    </div>
  </BrowserRouter>
}
```

**Very nice approach to use render function**

```js
const MatchWithFade = ({ component: Component, ...rest }) => (
  <Route {...rest} render={(matchProps) => {
    <FadeIn>
      <Component {...matchProps} />
    </FadeIn>
  }} />
)
```

## Rendering a Match

Match renders UI when a pattern matches a location.

`<Route>` is a component that determines whether or not to render a specified component based on the app's location.

```js
// Simplified <Route> implementation
const Route = ({ pattern, component: Component }) => {
  const pathname = window.location.pathname
  
  if (pathname.match(pattern)) {
    return <Component />
  } else {
    return null
  }
}
```

## Pattern Matching

```js
<Route path="/contracts" component={Contracts} />
<Route path="/contracts/current" component={CurrentContract} />
```

If you visit `/contracts/current`, both `<Contracts>` and `<CurrentContract>` components will render side by side.

This make sense as any number of components might match a given location and they will all render. `Match` does not impose any kind of exclusivity.

This pose a problem for `/` root URL where it will match everything.

## Exactly

Do not use exactly if you have nested routes or else refreshing will not work.

```js
<Route path="/e" component={Employment} />
```

## URL Hierarchy and Component Hierarchy

Does your application component tree reflect URL hierarchy?

## Transitioning

```js
Component.contextTypes = {
  router: object
}

// in your component, you can
this.context.router.transitionTo('/')
```

## Code splitting

* [**Route-based splitting vs Component-based splitting**](https://medium.com/@thejameskyle/react-loadable-2674c59de178#.kbvk273ju)
* [v2.1.0-beta.28 release note](https://github.com/webpack/webpack/releases/tag/v2.1.0-beta.28)
* [babel-plugin-syntax-dynamic-import](https://github.com/babel/babel/tree/master/packages/babel-plugin-syntax-dynamic-import)
* [DIY](https://twitter.com/ryanflorence/status/775743520615206913)
* [TC39 Proposal - Dynamic `import()`](https://github.com/tc39/proposal-dynamic-import)
* [Webpack Performance Budgets](https://github.com/webpack/webpack/issues/3216)
* [`System.import()` will be deprecated in webpack 3](https://github.com/webpack/webpack/issues/3098)
* [react-async-component](https://github.com/ctrlplusb/react-async-component)

**Use Babel plugin: `syntax-dynamic-import`**

```js
// Before
SystemJS.import('/js/main.js')
System.import('/js/main.js')
require('/js/main.js')
require.ensure(['/js/main.js'], cb)
myCustomNIHLoader('/js/main.js')

// Now
import main from '../js/main'

// Future - Dynamic import
// Stage-3
const AsyncModulePromise = import(
  '../js/lib/somethingNotNeededNow'
)
```

> Code splitting fixes the SPA Syndrome: Downloading the code for the Settings section when all you wanted was the About page.

Large JavaScript bundles will peg the main thread, taking longer to compile and run.

Splitting up your work into smaller chunks can get you closer to being interactive sooner, in particular when using HTTP/2. Only serving down the code a user needs for a route is just one pattern here [PRPL](https://developers.google.com/web/fundamentals/performance/prpl-pattern/).

Webpack treats `import()` as a split-point and puts the requested module in a separate chunk.

Make your main `<App>` simple and only have several <Route> to the routes. In this way you can then use code splitting easily and not concern with overlapping routes.

```js
// Inside <App>...
// When we navigate to "/", it will render the AsyncRoute and pass in a
// import() promise

<Provider store={store}>
  <Route
    exact
    path="/"
    component={(props) =>
      <AsyncRoute
        props={props}
        loadingPromise={import("./Landing")}
      />
    }
  />
  
  <Route...>
</Provider>
```

```js
// A HOC for code splitting
class AsyncRoute extends Component {
  constructor(props) {
    super(props)
    this.state = { loaded: false }
  }
  
  componentDidMount() {
    this.props.loadingPromise.then(module => {
      this.component = module.default // Due to CommonJS
      this.setState({ loaded: true })
    })
  }
  
  render() {
    if (this.state.loaded) {
      return <this.component {...this.props.props} />
    } else {
      return <Loading />
    }
  }
}
```

```js
// Other implementation
class LazyLoad extends Component {
  state = {
    AsyncModule: null
  }
  
  componentDidMount() {
    this.props.getComponent()
      .then(module => module.default)
      .then(AsyncModule => this.setState({AsyncModule}))
  }
  
  render() {
    const { loader, ...childProps } = this.props
    const { AsyncModule } = this.state
    
    if (AsyncModule) {
      return <AsyncModule {...childProps}>
    }
    
    if (loader) {
      const Loader = loader
      return <Loader>
    }
    
    return null
  }
}

// Using it
const MyComponent = () => {
  return <LazyLoad getComponent={() => import('./someFile.js')} />
}
```

## Scroll Management

* [Scroll management](https://github.com/ReactTraining/react-router/issues/3950#issuecomment-279293199)
* [Found](https://github.com/4Catalyzer/found)