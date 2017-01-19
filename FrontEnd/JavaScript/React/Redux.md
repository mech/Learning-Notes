# Redux

* [Jumpstate - simple and powerful state management utility for Redux (worth a look)](https://github.com/jumpsuit/jumpstate)
* [conventional-redux](https://github.com/mjaneczek/conventional-redux)
* [Practical Redux](http://blog.isquaredsoftware.com/2016/10/practical-redux-part-0-introduction/)

## Store

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

## Actions

Do not underestimate the power of action creator. It can help document your software by specifying what action a component can dispatch and this kind of information can be helpful in your team.

Our action creator always return an object, but it can also return a function:

```js
const signInUser = ({ email, password }) => (
  {
    type: 'SIGN_IN_USER',
    payload: { email, password }
  }
)

// Or
const signInUser = ({ email, password }) => (dispatch) => {
  fetch()
    .then(res => res.json)
    .then(data => dispatch())
}
```

## Effects

* [What is a thunk?](https://daveceddia.com/what-is-a-thunk/)
* [Idiomatic Redux: Thoughts on Thunks, Sagas, Abstraction, and Reusability](http://blog.isquaredsoftware.com/2017/01/idiomatic-redux-thoughts-on-thunks-sagas-abstraction-and-reusability/)
* [redux-loop](https://github.com/redux-loop/redux-loop)
* [redux-pack](https://github.com/lelandrichardson/redux-pack)

Isn't it funny that Redux's so-called "actions" don't actually do anything? They're just objects, boring and simple. Wouldn't it be cool if you could actually make them **do** something? Like, say, make an Ajax call, or trigger other actions? Because reducers are supposed to be pure we couldn't put that work inside a reducer. If you wanted an action to **do** something, that code would need to live inside a function. It would be nice if an action creator could return a function instead of an action object and that is what redux-thunk does. It is a simple middleware that looks at every action that passes through the system, and if it's a function, it calls that function. That's all it does.

Normally `dispatch()` accepts only action object. redux-thunk allows you to pass a function to `dispatch()`.

With redux-thunk, we are not limited to a single action, we can dispatches multiple actions down the pipeline to reducers.

## Middleware

Middleware has opportunity to log, stop, modify, or not touch an action.

```
View => Action Creator => Action => Middleware => Reducers => State
```

### API Middleware

The goal of API middleware is to do async operation so that by the time the action reaches the reducer, it should have been resolved already.

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

Reducer is our action handler. It is where update of state happens.

The reducer is (almost) synonymous with "store", so don't be surprise when people are referring them as the same thing.

> Loop took the approach of replicating the Elm model where the reducer becomes an update function exclusively responsible for inspecting the action log.

### Reducer Composition

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

`connect` is a higher order/curry function for generating a container component to let presentational component "connect" to the Redux Store.

connect function takes care of:

1. Subscribing and unsubscribing
2. Re-rendering
3. Getting state from `store.getState()`
4. Setup `contextTypes` for the `store`

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