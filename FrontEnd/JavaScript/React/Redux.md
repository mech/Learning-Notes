# Redux

> The main purpose of Redux is to isolate state management from I/O side effects.

* [Jumpstate - simple and powerful state management utility for Redux (worth a look)](https://github.com/jumpsuit/jumpstate)
* [conventional-redux](https://github.com/mjaneczek/conventional-redux)
* [Practical Redux](http://blog.isquaredsoftware.com/2016/10/practical-redux-part-0-introduction/)
* [Isn’t our code just the BEST - @fat](https://medium.com/bumpers/isnt-our-code-just-the-best-f028a78f33a9#.7xiqumcuk)
* [Redux best practices gotchas](https://getstream.io/blog/react-redux-best-practices-gotchas/)
* [React state management with Redux store](https://onsen.io/blog/react-state-management-redux-store/)
* [react-redux-realworld-example-app](https://github.com/gothinkster/react-redux-realworld-example-app)
* [What are the disadvantages of storing all your state in a single immutable atom?](https://github.com/reactjs/redux/issues/1385#issuecomment-290466442)
* [The SoundCloud Client in React + Redux](https://www.robinwieruch.de/the-soundcloud-client-in-react-redux/)

Redux helps us enforce good state boundary. You do not want to misapply it by storing form state in the store. It is not meant for that.

Redux solve React's data tunnelling problem.

> Change is not the result of one object acting on another (OOP-way); change is the result of a process (Reducer) being applied to an unchangeable atom.

Most actual code should be written as:

* Redux middleware
* Higher-order components

This means you should almost never write logic in a plain UI component.

> Make the rest of your components accept data without much validation. Then do your validation rigorously at the Store level. See [#9 The store is the component's servant](https://hackernoon.com/10-react-mini-patterns-c1da92f068c5#.7ev5n4sus)

Many moving parts:

* Store, state, reducers, action creators, actions, async actions, middleware, connected components

## Business Logic

* [Where do I put my business logic in a React-Redux application?](https://medium.com/@jeffbski/where-do-i-put-my-business-logic-in-a-react-redux-application-9253ef91ce1)

There are many kinds of logics:

* Business logic
* Domain logic
* Application logic
* UI logic
* Form logic

Business logic is naturally complex because of rules and many branches to consider.

Business logic in Redux is typically spread across selectors, reducers, action creators and thunks.

> Unfortunately in Redux, the reducer can only ever handle synchronous logic. So asynchronous "business logic" that depends on state either needs to get it from the component via dispatch (if the component has that info, which is not always), or through your orchestrator concept of your choice (thunk, sagas, epic), which have access to state for that.

> If it wasn't for the reducer's limitation, there would be no need for it. - [@Phoenixmatrix](https://github.com/reactjs/redux/issues/2295#issuecomment-287769785)

What is business logic?

* Business rules
* Validation, verification and correctness
* Compliance
* Complex calculation (rebates, payslip, rate, reimbursement)
* Permission, what user is allowed to do
* Processing (asynchronous orchestration) - waiting for response after making payment

## Code Organization

* [Scaling your Redux App with ducks](https://medium.com/@alexnm/scaling-your-redux-app-with-ducks-6115955638be#.1qa7z6y4d)
* [10 Tips for Better Redux Architecture](https://medium.com/javascript-scene/10-tips-for-better-redux-architecture-69250425af44#.p35g31etj)
* [Redux Architecture](https://github.com/jarvisaoieong/redux-architecture/blob/master/README.md)
* [Undirectional User Interface Architectures](http://staltz.com/unidirectional-user-interface-architectures.html)
* [ducks-modular-redux](https://github.com/erikras/ducks-modular-redux)
* [Things I wish I knew about Redux](https://medium.com/horrible-hacks/things-i-wish-i-knew-about-redux-9924abf2f9e0)
* [A Better File Structure For React/Redux Applications](https://marmelab.com/blog/2015/12/17/react-directory-structure.html)
* [Three Rules For Structuring (Redux) Applications](https://jaysoo.ca/2016/02/28/organizing-redux-application/)
* [Redux best practices](https://medium.com/lexical-labs-engineering/redux-best-practices-64d59775802e)

Function-first folders (e.g. `/container`, `/actions`, `/reducers`, `/components`) don't scale at all. As you add more features, you add files into the same folders.

```
duck/
├── actions.js
├── index.js
├── reducers.js
├── selectors.js
├── tests.js
├── types.js
├── utils.js
```

* **types** - action types names like `timesheet/CANCEL`
* **actions** - action creators and thunks
* **reducers** - don't be afraid to use `combineReducers` as much as needed
* **selectors** - the split between operations and selectors resembles the CQRS pattern. Selector functions take a slice of the application state and return some data based on that. They never introduce any changes to the application state.
* **index** - export the default reducers, export as named exports the action creators and export types if they are needed elsewhere.

Feature folder definitely make sense for isolated bounded-context kind of components. But for reducers, it may be difficult to know how the global state tree looks like.

## Authentication

* [Nice series to watch](https://www.youtube.com/watch?v=g8O0FT0uoDA&list=PLuNEz8XtB51K-x3bwCC9uNM_cxXaiCcRY&index=21#t=155.03974)

## Normalizr

Why do we need it? Our JSON API may be deeply nested and duplicative. We want to coerce that deep API into more manageable and cacheable ID-indexed objects.

We then pass the normalized records to reducers. Reducers should only store these. When reducers only store normalized records it becomes super easy to query using Reselect.

```js
// from this:
{
  "id": "123",
  "name": "mech"
}

// to this
{
  "result": "123",
  "entities": {
    "users": {
      "123": {
        "name": "mech"
      }
    }
  }
}
```

https://medium.com/@mark.erikson/having-an-entities-slice-is-very-normal-60917516291f#.8hjj34h2y

## Store

> Redux gets easier once I treat it as a plain **database**:

> I tell Redux the initial state, and how an action (**event**) affects the state of the application. (Like database schema and stored procedures.)

> Then Redux takes care of managing it and notifying the listeners, and provides ways to inspect and debug the state.

> For me that's all Redux is to me (I wouldn't expect a database to make an HTTP call). For I/O and asynchronous stuff, I perform it outside Redux. This keeps my Redux store predictable. The type signature is always `store.dispatch(actionObject)`. No dispatching functions and no hidden meaning inside the action (e.g. dispatching an action will not make an API call).

```js
// Simplify Redux's store implementation
// Using Factory Pattern
function createStore(reducer, initialState) {
  // Closure - private variables
  let state = initialState
  let isDispatching = false
  
  const getState = () => (state)
  
  const dispatch = (action) => {
    if (isDispatching) throw new Error('Cannot dispatch while still dispatching')
    
    try {
      isDispatching = true
      state = reducer(state, action)
    } finally {
      isDispatching = false
    }
  }
  
  return {
    getState,
    dispatch
  }
}
```

```js
// ??
const createStoreWithMiddleware = applyMiddleware()(createStore)
const store = createStoreWithMiddleware(reducer)
```

```js
const configureStore = () => {
  const middleware = [promise]
  if (process.env.NODE_ENV !== 'production') {
    middleware.push(createLogger())
  }
  
  return createStore(
    todoApp,
    applyMiddleware(...middleware)
  )
}
```

### Store Enhancer

* [Alternate Proof of Concept: Enhancer Overhaul](https://github.com/reactjs/redux/pull/2214)

## Provider

Distant leaf components need access to state that intermediary components don't need.

```js
<BrowserRouter>
  <Provider store={store}>
    <div className="app">
      <Match pattern="/" component={Landing} />
    </div>
  </Provider>
</BrowserRouter>

// Or
<Provider store={store}>
  <Router>
    <Route />
  </Router>
</Provider>
```

## Actions

> Action creators are not inherent part of Redux - Dan Abramov

* [Idiomatic Redux: Why use action creators?](http://blog.isquaredsoftware.com/2016/10/idiomatic-redux-why-use-action-creators/)

Note that same action can be handled by several reducers.

> The one most valuable thing that made Redux so much easier for me is treating actions as **events** and not **commands**. This completely eliminates the struggle to decide how to design actions and what to put in them. - [@aikoven](https://github.com/reactjs/redux/issues/2295#issuecomment-287734255)

Action describes something has (or should) happen, but did not say how it should be done. It is completely serializable as an intent.

But what happen if you want to debounce/buffer/throttle it?

You can combine the action types with action creators:

```js
// Note the 2 export here... we do not need separate types.js file just for the constants
export const SET_GRID_SIZE = 'SET_GRID_SIZE'

export const setGridSize = ({width, height}) => ({
  type: SET_GRID_SIZE,
  width,
  height
})
```

Do not underestimate the power of action creator. It can help document your software by specifying what action a component can dispatch and this kind of information can be helpful in your team.

Our action creator always return an object, but it can also return a function:

```js
const signInUser = ({ email, password }) => (
  {
    type: 'SIGN_IN_USER',
    payload: { email, password }
  }
)

// Or with redux-thunk
const signInUser = ({ email, password }) => (dispatch) => {
  fetch()
    .then(res => res.json)
    .then(data => dispatch())
}
```

There is no need for action creators to be pure, but it certainly help with testing when it is pure.

A Promise is just an object with no side effects until `.then()` is called on it. So, returning a Promise from an action creator still retains its purity.

You can return things from thunks. Returning Promises from thunks is useful, because then you can chain together async functions. See [Composition on redux-thunk](https://github.com/gaearon/redux-thunk#composition)

## Effects

* [What is a thunk?](https://daveceddia.com/what-is-a-thunk/)
* [Idiomatic Redux: Thoughts on Thunks, Sagas, Abstraction, and Reusability](http://blog.isquaredsoftware.com/2017/01/idiomatic-redux-thoughts-on-thunks-sagas-abstraction-and-reusability/)
* [redux-loop](https://github.com/redux-loop/redux-loop)
* [redux-pack](https://github.com/lelandrichardson/redux-pack)
* [Redux Side Effects](https://github.com/markerikson/react-redux-links/blob/master/redux-side-effects.md)

Isn't it funny that Redux's so-called "actions" don't actually do anything? They're just objects, boring and simple. Wouldn't it be cool if you could actually make them **do** something? Like, say, make an Ajax call, or trigger other actions? Because reducers are supposed to be pure we couldn't put that work inside a reducer. If you wanted an action to **do** something, that code would need to live inside a function. It would be nice if an action creator could return a function instead of an action object and that is what redux-thunk does. It is a simple middleware that looks at every action that passes through the system, and if it's a function, it calls that function. That's all it does.

Normally `dispatch()` accepts only action object. redux-thunk allows you to pass a function to `dispatch()`.

With redux-thunk, we are not limited to a single action, we can dispatches multiple actions down the pipeline to reducers.

```js
// just in case you want to directly access the API
// which allow your thunk to have access to all your API endpoint calls
applyMiddleware(thunk.withExtraArgument(api), ...others)

// then at your async actions:
export const fetchUserByEmail = (email) => {
  return (dispatch, getState, api) => {
    // prevent race condition
    if (getIsFetching(getState())) {
      return Promise.resolve()
    }    

    dispatch(setIsFetching())
    return api.fetchUserByEmail(email)
      .then(api.checkStatus)
      .then(api.toJSON)
      .then(response => normalize(response.user, schema.user))
      .then(response => dispatch(setUser(response)))
      .catch(api.handleError(dispatch))
  }
}
```

## Middleware

* [Why do we need middleware for async flow in Redux?](https://stackoverflow.com/questions/34570758/why-do-we-need-middleware-for-async-flow-in-redux/)

Middleware has opportunity to log, stop, modify, or not touch an action.

```
View => Action Creator => Action => Middleware => Reducers => State (Store)
```

### API Middleware

* [Redux 4 Ways - Comparison of thunk, saga, observable and promise middleware](https://medium.com/react-native-training/redux-4-ways-95a130da0cdc#.ev3d5xmwj)
* [redux-api-middleware](https://github.com/agraboso/redux-api-middleware)
* [redux-promise](https://github.com/acdlite/redux-promise)
* [redux-promises](https://github.com/CrocoDillon/redux-promises)
* [redux-promise-middleware](https://github.com/pburtchaell/redux-promise-middleware)
* [redux-axios-middleware](https://github.com/svrcekmichal/redux-axios-middleware)

The goal of API middleware is to do async operation so that by the time the action reaches the reducer, it should have been resolved already.

The action is a specially packaged "API action" with `type='API'` maybe? It would be handled by a middleware that understand this type and proceed to use fetch API and do async request.

```js
export default function({ dispatch }) {
  return next => action => {
    if (!action.payload || !action.payload.then) {
      return next(action)
    }
    
    // make sure the action's promise resolves
    action.payload
      .then(function(response) {
        // create a new action with the old type, but
        // replace the promise with the response data
        const newAction = { ...action, payload: response }
        dispatch(newAction)
      })
  }
}
```

You can use middleware to:

* Massage data - Like from AMS JSON API to client-side model format
* Authorization

## Reducers

* [Structuring Reducers](https://github.com/markerikson/redux/blob/structuring-reducers-page/docs/recipes/StructuringReducers.md)
* [Generating Reducers](http://redux.js.org/docs/recipes/ReducingBoilerplate.html#generating-reducers)

Reducer is our action handler. It is where update of state happens. Reducer exists to specify how the state tree is **transformed** by actions. Reducer is a transformation function.

The reducer is (almost) synonymous with "store", so don't be surprise when people are referring them as the same thing.

> Loop took the approach of replicating the Elm model where the reducer becomes an update function exclusively responsible for inspecting the action log.

### replaceReducer

* [Dispatch INIT after replaceReducer](https://github.com/reactjs/redux/issues/350)
* [How to dynamically load reducers for code splitting in a Redux application?](https://stackoverflow.com/questions/32968016/how-to-dynamically-load-reducers-for-code-splitting-in-a-redux-application)
* [redux-injector](https://github.com/randallknutson/redux-injector)

Don't confuse between state tree and reducers. They are 2 separate things. You can retain your state tree while swapping out reducers during code splitting.

### Reducer Composition

* [Feature Request: Allow reducers to consult global state](https://github.com/reactjs/redux/pull/1768)
* [RFC: Make combineReducers() shape-agnostic](https://github.com/reactjs/redux/issues/1792)

Break up state management into smaller, more focused chunk to handle a subset of the app's state and actions.

> Notice how this simplifies the logic for handling `OPEN_THREAD`. Before, our logic had to consider the entire state tree.

```js
const todo = (state, action) => {
  switch (action.type) {
    case 'ADD_TODO':
      return {
        id: action.id,
        text: action.text,
        completed: false
      }
    case 'TOGGLE_TO':
      if (state.id !== action.id) {
        return state
      }
      
      return {
        ...state,
        completed: !state.completed
      }
    default:
      return state
  }
}

const todos = (state = [], action) => {
  switch (action.type) {
    case 'ADD_TODO':
      return [
        ...state,
        todo(undefined, action)
      ]
    case 'TOGGLE_TO':
      return state.map(t => todo(t, action))
    default:
      return state
  }
}
```

```js
// Simplify combineReducers implementation
const combineReducers = (reducers) => {
  // Since the returned function is a root reducer
  return (state = {}, action) => {
    return Object.keys(reducers).reduce((nextState, key) => {
      nextState[key] = reducers[key](state[key], action)
      return nextState
    }
    , {})
  }
}
```

You can use `combineReducers` multiple times in different files. You do not need to only use it at the root level.

### Reducer Factories

```js
const { makeIndicator, makePayloadAssignor } from '../shared/reducers'

const searchModule = combineReducers({
  searching: makeIndicator(c.SEARCH),
  results: makePayloadAssignor(c.SEARCH_RESPONSE, [])
});
```

### Higher Order Reducers

```js
// next, prev and paginate are all reducers
const next = (state) => state.set('page', state.get('page') + 1)
const prev = (state) => state.set('page', Math.max(1, state.get('page') - 1))

const paginate = (id) => {
  return resolveEach(initialState, {
    [resolveActionType(actionTypes.NEXT), id]: next,
    [resolveActionType(actionTypes.PREV), id]: prev
  })
}

// Later at the combineReducers
export default combineReducers({
  recipesPager: paginate('recipes'),
  todos,
  recipes
})
```

## Connect

* [Recommended usage of `connect()`](https://github.com/reactjs/redux/issues/419)

`connect` is a higher order/curry function for generating a container component to let presentational component "connect" to the Redux Store.

connect function takes care of:

1. Subscribing and unsubscribing
2. Re-rendering (`forceUpdate`)
3. Getting state from `store.getState()`
4. Setup `contextTypes` for the `store`
5. Convert Redux state into React props with `mapState`. Allowing you to get a subset of state you care about for that component.

```js
// Container component
class ContainerComponent extends Component {
  componentDidMount() {
    const { store } = this.context
    this.unsubscribe = store.subscribe(() => this.forceUpdate())
  }
  
  componentWillUnmount() {
    this.unsubscribe()
  }
  
  render() {
    const props = this.props
    const { store } = this.context
    const state = store.getState()
    
    return (
      <PresentationComponent {...props} {...state}>
    )
  }
}

ContainerComponent.contextTypes = {
  store: React.PropTypes.object
}
```

Why do we need `connect`?

```js
// We can see all of the child components need some state and behaviors passed down
// connect can help us to separate such manual passing down of props
// connect also help us to do all the subscribing and forceUpdating
const TodoApp = () => (
  <AddTodo onAddClick={} />
  <TodoList todos={} />
  <Footer onFilterClick={} />
)

render(<TodoApp {...store.getState()} />)
store.subscribe(render)
render()
```

How to use it:

```js
const ContainerComponent = connect(
  mapStateToProps,
  mapDispatchToProps
)(PresentationalComponent)
```

Stateless functional connect:

```js
// Note that the prop-function is dispatch from store
let AddTodo = ({ dispatch }) => {
  let input
  
  return (
    <div>
     <input ref={node => input = node} />
     <button onClick={() => {
        dispatch({
          type: 'ADD_TODO',
          text: input.value
        })
        input.value = ''
      }}>
        Add Todo
      </button>
    <div>
  )
}

// Since it is `let`, we can reassign it
AddTodo = connect(
  state => { return {} },
  dispatch => { return { dispatch } }
)(AddTodo)

// Same as
// Note that this does not subscribe to the store since state is null
AddTodo = connect(null, null)(AddTodo)

// Same as, `dispatch` is automatically available
AddTodo = connect()(AddTodo)
```

```js
const mapStateToProps = (state, ownProps) => ({
  todos: state.todos,
  active: ownProps.filter === state.visibilityFilter
})

const mapDispatchToProps = (dispatch, ownProps) => ({
  onTodoClick(id) {
    dispatch(toggleTodo(id))
  },
})
```

You can also pass whole actions into `mapDispatchToProps` which will make that function dispatch-able. Redux will modify it to add a `dispatch()` so there is no need for you to call `this.props.dispatch()` yourself.

```js
import * as actions from './actions'

connect(null, actions)(App)

// Here you will find that actions exported function will become:

function () {
  return dispatch(actionCreator.apply(undefined, arguments));
}
```

## Selectors - State Transformation

* [Choose wisely (a fun introduction to reselect.js)](https://decembersoft.com/posts/redux-hero-part-3-choose-wisely-a-fun-introduction-to-reselect-js/)
* [Use reselect sparingly](https://medium.com/@yungsql/daf5a53bb93a)

Every component you write has different needs. Some might show data in the same format as your API, while others might need to amend, blend or selectively combine data for its UI.

Classically components get state directly from the store. Reselect queries and transforms data for each component.

```js
// For simple computation, it is totally fine to not use reselect
function mapStateToPros(state) {
  return {
    isShown: state.list.length > 0
  }
}

// We use getVisibleTodos() to "select" a "slice" of the todos we want
const mapStateToProps = (state, { params }) => ({
  todos: getVisibleTodos(state.todos, params.filter)
})

// We can move it to the reducer file
export default todos

export const getVisibleTodos = (todos, filter) => {
}
```

## Recompose

* [Why The Hipsters Recompose Everything](https://medium.com/javascript-inside/why-the-hipsters-recompose-everything-23ac08748198#.91wws275y)

## Redux with Flowtype

* [redux-thunk-flow: A working example on how to use Redux with redux-thunk and 100% flow coverage](https://github.com/hmeerlo/redux-thunk-flow)
* [Typed Redux](https://blog.callstack.io/typed-redux-2aa8bff926ff)
* [Type-checking React and Redux (+Thunk) with Flow — Part 1](https://blog.callstack.io/type-checking-react-and-redux-thunk-with-flow-part-1-ad12de935c36)
* [Redux and Flowtype](https://medium.com/@cdebotton/redux-and-flowtype-69ff1dd09036)
* [Using Redux with Flow](http://frantic.im/using-redux-with-flow)

```js
// Type-check Actions

// Using disjoint union type is much better than using constants for actions
// Disjoint union is tagged by a single property like 'type' here
export type Action =
  | { type: 'INCREMENT', payload: number }
  | { type: 'DECREMENT', payload: number }
  
const reducer = (state: State = initialState, action: Action): State => {
}

// We need to support dispatching thunk along with plain actions also

import type {
  Store as ReduxStore,
  Dispatch as ReduxDispatch
} from 'redux'



const mapDispatchToProps = (dispatch: *) => ({
})
```

## Take Latest and Debouncing

* redux-observable
* redux-saga

```js
// only load data for the last clicked
.flatmapLatest()

// Saga
function* watch() {
  yield* takeLatest('USER_FETCH', fetchUser)
}
```