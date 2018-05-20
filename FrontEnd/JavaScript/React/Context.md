# Context

* [Nested Provider example](https://codesandbox.io/s/9zj452q1yo)
* [Migrating to React's New Context API](https://blog.kentcdodds.com/migrating-to-reacts-new-context-api-b15dc7a31ea0)
* [Let's talk about Context](http://reactcontext.com/)
* [react-adopt - Compose render props components like a pro](https://github.com/pedronauck/react-adopt)

https://twitter.com/ryanflorence/status/981179212147998721

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

