# Context

* [Nested Provider example](https://codesandbox.io/s/9zj452q1yo)
* [Migrating to React's New Context API](https://blog.kentcdodds.com/migrating-to-reacts-new-context-api-b15dc7a31ea0)
* [Let's talk about Context](http://reactcontext.com/)
* [react-adopt - Compose render props components like a pro](https://github.com/pedronauck/react-adopt)
* [Prop Drilling](https://buttondown.email/kentcdodds/archive/8e22429d-fcc7-4d5b-af0b-3880c64a9857)
* [How to create react-tabs using ContextAPI](https://medium.com/dailyjs/how-to-create-react-tabs-using-contextapi-932c7bec35c7)
* [How To Master Advanced React Design Patterns: Context API](https://itnext.io/using-advanced-design-patterns-to-create-flexible-and-reusable-react-components-part-2-react-3c5662b997ab)
* [React 16.3 is out and with it comes the officially supported Context API](https://itnext.io/compound-components-with-react-v16-3-6679c752bd56)
* [How to protect your routes with React Context](https://medium.freecodecamp.org/how-to-protect-your-routes-with-react-context-717670c4713a)
* [How to build your own React-Router with new React Context Api](https://medium.com/@stevenkoch/how-to-build-your-own-react-router-with-new-react-context-api-1647406b9b93)
* [React Context in the World of Component Composition](https://medium.com/@ablamunits/react-context-in-the-world-of-component-composition-ce049d99afd9)
* [What can the React Context API do for you? Multi-language text, Modals, and Themes](https://codeburst.io/what-can-react-context-api-do-for-you-multi-language-text-modals-and-theme-switchers-9cfbc8e5ee5e)

https://twitter.com/ryanflorence/status/981179212147998721

```js
const defaultProviderValue = {
  onItemClick: () => null,
  selectedItems: []
}

const { Provider, Consumer } = React.createContext(defaultProviderValue)

class Parent extends Component {
  state = {
    selectedItems: []
  }
  
  render() {
    const contextValue = {
      onItemClick: this.onItemClick,
      selectedItems: this.state.selectedItems
    }
    
    return (
      <Provider value={contextValue}>
        {this.props.children}
      </Provider>
    )
  }
}

class Item extends Component {
  renderItem = (context) => {
  }
  
  render() {
    return (
      <Consumer>
        {(context) => this.renderItem(context)}
      </Consumer>
    )
  }
}

class Usage extends Component {
  render() {
    return (
      <Parent>
        <Item />
        <Item />
      </Parent>
    )
  }
}
```

## Deprecated

* [react-contextual](https://github.com/drcmda/react-contextual)
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

