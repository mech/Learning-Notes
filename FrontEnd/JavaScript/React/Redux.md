# Redux

* [Microsoft's Satchel.js](https://github.com/Microsoft/satcheljs)

> Premature optimisation is the root of all evil. While I still hold true to this quote, I believe that implementing Redux in most React applications **early on** is the right approach. From our experience, the point where just using local state becomes cumbersome happens pretty quickly.

---

> The command pattern, event sourcing, and Redux are all different architectures, but they all accomplish a similar goal: transactional state management.
> 
> What is revolutionary about Redux architecture is how it standardized the process of managing transactional state with reducers. In that sense, it applies the idea of transactional state to a particular context and demonstrates how reducer functions over action objects (events) can be the single source of truth for the application state.
> 
> Event sourcing never did anything of the sort. It does not prescribe how events are handled, only their creation and recording.
>
> Typical event sourcing implementations were a mix of object-oriented and imperative code. Event objects were commonly applied with polymorphic methods, and separately persisted with object serializers. Side effects were common.
>
> By encoding the action type in the message, and keeping the action object itself completely unaware of the objects on which it acts and methods being called, Redux action objects serialize easier. Reducers generalize easier. - [](https://medium.com/@_ericelliott/the-command-pattern-event-sourcing-and-redux-are-all-different-architectures-but-they-all-3e36b70cbc60)

---

> The main purpose of Redux is to isolate state management from I/O side effects.

* [Idiomatic Redux: The Tao of Redux, Part 1 - Implementation and Intent](http://blog.isquaredsoftware.com/2017/05/idiomatic-redux-tao-of-redux-part-1/)
* [Finally understand Redux by building your own Store](https://toddmotto.com/redux-typescript-store)
* [Debounce Your React and Redux Code to Improve Performance](https://medium.com/gitconnected/debounce-react-and-redux-code-for-improved-performance-4b8d3c19e305)
* [Redux Resource](https://redux-resource.js.org/)
* [A good overview of Redux](https://medium.com/@nicotsou/tltr-redux-e4fc30f87e4a)
* [Redux Architecture Guidelines](http://joeellis.la/redux-architecture/)
* [Redux Architecture and Best Practices](https://github.com/markerikson/react-redux-links/blob/master/redux-architecture.md)
* [Dissecting Twitter’s Redux Store](https://medium.com/statuscode/dissecting-twitters-redux-store-d7280b62c6b1)
* [Diving Deeper into Twitter’s Redux Store: Adventures in Minified Vendor Javascript](https://medium.com/@nuncamind/diving-deeper-into-twitters-redux-store-adventures-in-minified-vendor-javascript-67fbac5dc219)
* [What's So Great About Redux?](https://medium.com/@modernserf/whats-so-great-about-redux-ac16f1cc0f8b)
* [mobx-state-tree](https://github.com/mobxjs/mobx-state-tree)
* [Redux or MobX: An attempt to dissolve the Confusion](https://www.robinwieruch.de/redux-mobx-confusion/)
* [Redux for state management in large web apps](https://www.mapbox.com/blog/redux-for-state-management-in-large-web-apps/)
* [Jumpstate - simple and powerful state management utility for Redux (worth a look)](https://github.com/jumpsuit/jumpstate)
* [conventional-redux](https://github.com/mjaneczek/conventional-redux)
* [Practical Redux](http://blog.isquaredsoftware.com/2016/10/practical-redux-part-0-introduction/)
* [Isn’t our code just the BEST - @fat](https://medium.com/bumpers/isnt-our-code-just-the-best-f028a78f33a9#.7xiqumcuk)
* [Redux best practices gotchas](https://getstream.io/blog/react-redux-best-practices-gotchas/)
* [React state management with Redux store](https://onsen.io/blog/react-state-management-redux-store/)
* [react-redux-realworld-example-app](https://github.com/gothinkster/react-redux-realworld-example-app)
* [What are the disadvantages of storing all your state in a single immutable atom?](https://github.com/reactjs/redux/issues/1385#issuecomment-290466442)
* [The SoundCloud Client in React + Redux](https://www.robinwieruch.de/the-soundcloud-client-in-react-redux/)
* [What is the right way to do asynchronous operations in Redux?](https://decembersoft.com/posts/what-is-the-right-way-to-do-asynchronous-operations-in-redux/)
* [Some Redux Internals](https://medium.com/@jankjr_/dissecting-redux-864039c6cf59)
* [How to make your React app fully functional, fully reactive, and able to handle all those crazy side effects](https://medium.freecodecamp.org/how-to-make-your-react-app-fully-functional-fully-reactive-and-able-to-handle-all-those-crazy-e5da8e7dac10)
* [How to use React's Provider Pattern](https://www.robinwieruch.de/react-provider-pattern-context/)

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

## Against Redux

* [**How to manage or eliminate React state without Redux**](http://monicalent.com/blog/2017/07/23/manage-state-in-react/)
* [Repatch - the simplified Redux](https://community.risingstack.com/repatch-the-simplified-redux/)
* [Simplifying Redux Architecture](https://medium.com/@TuckerConnelly/simplifying-redux-architecture-cd50426c941a)
* [The road to Redux and back - Why I decided to go back to vanilla React](https://medium.freecodecamp.org/the-road-to-redux-and-back-d9987c7bb894)

## Performance

* [Redux isn't slow, you're just doing it wrong - An optimization guide](https://reactrocket.com/post/react-redux-optimization/)

## State Shape

> Do not store object in Redux. Use plain primitive and serialize it into model object at client side instead.

* [Why not to store objects in Redux](https://medium.com/collaborne-engineering/why-not-to-store-objects-in-redux-7f41243020fc)

3 approaches:

1. The Nested Object
2. The Nested Reference - flat
3. The Separated Object - flat

While all the approaches have their upsides and downsides, we will quickly discover that in Redux, keeping the structure as **flat and normalized** as possible (as in the second and third approaches) makes the code cleaner and simpler.

```js
// Nested Object
state = {
  recipes: [
    {
      name: 'omelette',
      ingredients: [
        { name, quantity }
      ]
    }
  ]
}

// Nested Reference - Flat and Normalized
// Use of 2 reducers for recipes and ingredients possible
// since we can process them independently
state = {
  recipes: [
    {
      name: 'omelette',
      ingredients: [2, 3]
    }
  ],
  ingredients: {
    2: { name, quantity },
    3: { name, quantity }
  }
}
```

Treat your state as a database and design it separately from the presentation or logic layers.

## Compared to MobX and @nx-js/observer-util

* [Some complaints](https://news.ycombinator.com/item?id=12975737)
* Redux often end up with very extensive lists of props. MobX generally get away with just passing in the model itself. You actions are just methods on the model class.
* [react-easy-state is using @nx-js/observer-util under the hood](https://github.com/solkimicreb/react-easy-state)
* [Writing a JavaScript Framework - Data Binding with ES6 Proxies](https://blog.risingstack.com/writing-a-javascript-framework-data-binding-es6-proxy/)

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

## @@INIT

After the store is initialized but right before it's returned, `createStore()` actually dispatches an initialization action:

```js
// Ensure all states are undefined, thus you can use default
// parameter to define some initial state
dispatch({ type: '@@redux/INIT' })
```

@@INIT is launched twice on purpose.

When the store is created, Redux immediately calls the reducers and uses their return values as initial state. This first call to the reducer sends `undefined` for the state.

Note: The 2nd argument to `createStore` should only use for state hydration and not for initializing state.

## Code Organization

* [How I organize my React & Redux projects](https://medium.com/@bruno__quaresma/how-i-organize-my-react-redux-projects-602990f6d0f0)
* [A feature based approach to React development](http://ryanlanciaux.com/blog/2017/08/20/a-feature-based-approach-to-react-development/)
* [react_feature_folder_example](https://github.com/ryanlanciaux/react_feature_folder_example)

```
src/
├── Login/     => Login feature
  ├── index.js => Public API
  ├── components/
  ├── actions/
  ├── reducers/
  ├── selectors/
├── Projects/
├── shared/
  ├── reducers.js
```

It's generally a good idea to reference any part of a feature through the feature's `index.js` rather than the file directly. This treats the index as each feature's API contract and quickly illuminates any issues that may occur with any refactoring.

**Code is easier to refactor** - If a feature has one entry point, it's clear that removing the feature will have limited impact on the rest of the system. Additionally, if changes are made to a Login feature, they should have no impact on a Project feature.

```
src/
├── components/ => Reusable components like <Input>, <Calendar>
├── pages/      => Screens that are application-specific
├── utils/      => Logic that are not about the application domain like String/Array operation
├── redux/      => Redux state management code, arranged by features
  ├── feature_name/
    ├── actions.js
    ├── reducers.js
    ├── types.js
```

```js
// Try putting your actions and reducer into one file

const ADD = 'cart/ADD'

export default function cart(state, action) {
}

export function add() {
  return {
    type: ADD
  }
}
```

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

* A very flat structure
* All entities have their ID and separate tables
* [Using Normalizr to organize data in stores - practical guide](https://hackernoon.com/using-normalizr-to-organize-data-in-stores-practical-guide-82fa061b60fb)

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

```js
// Using reduce() to tag ID
const colors = [
  {
    id: '-xekare',
    title: 'rad red',
    rating: 3
  }
]

const hashColors = colors.reduce(
  (hash, {id, title, rating}) => {
    hash[id] = {title, rating}
    return hash
  },
  {}
)

// Result, the ID is being used as the key now for better findability
{
  "-xekare": {
    title: 'rad red',
    rating: 3
  }
}

// Use Object.values() to loop through
// We do not need the keys, just values
render() {
  return (
    {Object.values(props.colors).map(color =>
      <Color color={color} />
    )}
  )
}
```

## Store

* Where state are stored
* Only the store has access to the reducer

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

```js
const enhancer = compose(
  applyMiddleware(
    thunk,
    socketMiddleware,
    logger
  ),
  DevTools.instrument()
)
```

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

* [redux-define](https://github.com/smeijer/redux-define)
* [redux-act](https://github.com/pauldijou/redux-act)

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

Reducers are services that modify state. Middlewares modify actions. Unlike reducers, middleware can modify, stop/supress, or add more actions, and just actions.

Interceptors for actions.

Since the middleware have access to the actions, the `dispatch()` function, and the store, they are the **most versatile and powerful** entities in Redux.

In some cases, middleware might suppress actions or change them. That is why **implementing a logger in a reducer** is not a viable solution: some of the actions might not reach it.

> Side effect is mostly done at middleware

The action passes through the store's chain of middlewares, where actions may be intercepted and additional behaviour may be executed. Middlewares are commonly used to handle side-effects in Redux applications.

* [Why do we need middleware for async flow in Redux?](https://stackoverflow.com/questions/34570758/why-do-we-need-middleware-for-async-flow-in-redux/)
* [You aren't using middleware enough](https://medium.com/@jacobp100/you-arent-using-redux-middleware-enough-94ffe991e6)

Middleware has opportunity to log, stop, modify, or not touch an action.

```
View => Action Creator => Action => Middleware => Reducers => State (Store)
```

### Authorization Middleware

Since to perform a task involve dispatching an action. And action can be stopped using middleware. Middleware is a good place to enforce authorization and permission related tasks.

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

Think of reducers as "Services". You have a RecipeBook service, an Ingredient service, Authentication service, etc. Each of these services are their own reducers that manages just that slice of the data. Some actions can affect more than more service.

Function that manage application state by listening to particular actions.

* [Structuring Reducers](https://github.com/markerikson/redux/blob/structuring-reducers-page/docs/recipes/StructuringReducers.md)
* [Generating Reducers](http://redux.js.org/docs/recipes/ReducingBoilerplate.html#generating-reducers)

Reducer is our action handler. It is where update of state happens. Reducer exists to specify how the state tree is **transformed** by actions. Reducer is a transformation function.

The reducer is (almost) synonymous with "store", so don't be surprise when people are referring them as the same thing.

> Loop took the approach of replicating the Elm model where the reducer becomes an update function exclusively responsible for inspecting the action log.

### replaceReducer

* [Dispatch INIT after replaceReducer](https://github.com/reactjs/redux/issues/350)
* [How to dynamically load reducers for code splitting in a Redux application?](https://stackoverflow.com/questions/32968016/how-to-dynamically-load-reducers-for-code-splitting-in-a-redux-application)
* [redux-injector](https://github.com/randallknutson/redux-injector)
* [SO - How to dynamically load reducers for code splitting in a Redux application?](https://stackoverflow.com/questions/32968016/how-to-dynamically-load-reducers-for-code-splitting-in-a-redux-application/33044701#33044701)

Don't confuse between state tree and reducers. They are 2 separate things. You can retain your state tree while swapping out reducers during code splitting.

### Reducer Composition

If you only have a single root reducer, you will find that it is taking care of different parts of the state tree. It is carrying too much responsibilities and frankly hard to maintain.

* [Feature Request: Allow reducers to consult global state](https://github.com/reactjs/redux/pull/1768)
* [RFC: Make combineReducers() shape-agnostic](https://github.com/reactjs/redux/issues/1792)

---

**Disadvantages of combineReducer**

* Single reducer can't work with multiple slices of state
* Does not work on non-object states
* Does not work with immutable.js-based states

---

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
* [connect.js explained](https://gist.github.com/gaearon/1d19088790e70ac32ea636c025ba424e)

`connect` is a higher order/curry function for generating a container component to let presentational component "connect" to the Redux Store.

**Note:** It is okay to have a bit of logic at `mapStateToProps` like selecting the right state slice (selector) or filtering etc.

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

> Selectors work well with `getState` inside of a thunk

A caching and memoization strategy. Calculation only happen when a change happens in a related part of the state tree.

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

More examples of selectors:

```js
// A basic selector - get a property of the state
const channelsSelector = (state) => {
  state.get('channels')
}

// A curried selector - method which returns a selector that only
// finds an element with a given ID
const channelSelector = (id) => (state) => {
  state.get('channels').find(c => c.get('id') === id)
}

// A Reselect selector - parameters of final argument are the
// results of the first two
import { createSelector } from 'reselect'

const activeChannelSelector = createSelector(
  state => state.get('activeChannel'),
  state => state.get('channels'),
  (activeChannel, channels) => {
    return channels.find(c => c.get('id') === activeChannel)
  }
)
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

## Examples

* [reddit-mobile](https://github.com/reddit/reddit-mobile)

## Books

* [Advanced Redux (DONE)](https://app.pluralsight.com/library/courses/advanced-redux/table-of-contents)
* The Complete Redux Book - Page 60/179
* Redux from Scratch - Page 55/268
