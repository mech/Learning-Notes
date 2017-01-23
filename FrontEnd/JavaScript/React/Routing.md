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
      <Match exactly pattern="/" component={HomeContainer} />
      <Match exactly pattern="/r/:name" component={SubredditContainer} />
      <Match pattern="/one" render={() => <h2>One</h2>} />
      <Match pattern="/re" render={() => (<Redirect to="/10/20" />)} />
    </div>
  </BrowserRouter>
}
```

**Very nice approach to use render function**

```js
const MatchWithFade = ({ component: Component, ...rest }) => (
  <Match {...rest} render={(matchProps) => {
    <FadeIn>
      <Component {...matchProps} />
    </FadeIn>
  }} />
)
```

## Rendering a Match

Match renders UI when a pattern matches a location.

`<Match>` is a component that determines whether or not to render a specified component based on the app's location.

```js
// Simplified <Match> implementation
const Match = ({ pattern, component: Component }) => {
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
<Match pattern="/contracts" component={Contracts} />
<Match pattern="/contracts/current" component={CurrentContract} />
```

If you visit `/contracts/current`, both `<Contracts>` and `<CurrentContract>` components will render side by side.

This make sense as any number of components might match a given location and they will all render. `Match` does not impose any kind of exclusivity.

This pose a problem for `/` root URL where it will match everything.

## Exactly

Do not use exactly if you have nested routes or else refreshing will not work.

```js
<Match pattern="/e" component={Employment} />
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

* [DIY](https://twitter.com/ryanflorence/status/775743520615206913)