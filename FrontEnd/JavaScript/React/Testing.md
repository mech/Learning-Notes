# React Testing

* [A guide to TDD a React/Redux TodoList App — Part 1](https://hackernoon.com/a-guide-to-tdd-a-react-redux-todolist-app-part-1-b8a200bb7091)

When to test?

* Test business logic using Jest unit test.
* Use Snapshot Testing for React Structural Test - `react-test-renderer`

## Jest

While Jest provides browser globals such as window thanks to jsdom, they are only approximations of the real browser behavior.

Jest is intended to be used for unit tests of your logic and your components rather than the DOM quirks.

* No longer need `__tests__/` folder
* Auto-mocking is turned off
* Using Jasmine's assertion library
* Look for file matching `*.test.js` or `*.spec.js`

```js
// toBe() matcher using triple equal === for equality
expect(true).toBe(true)

// toEqual() is more sophisticated in matching
expect(a).toEqual({ name: 'Atomic' })
```

### Describe and It

`describe()` is used to organize assertions that all pertain to the same feature or context.

`it()` blocks are individual assertions or specs.

`describe()` block don't contain assertions, `it()` blocks do.

```js
describe('My first test', () => {
  let wrapper
  
  beforeEach(() => {
    wrapper = shallow(<App />)
  })

  it('is true', () => {
    expect(true).toBe(true)
  })
  
  describe('Another context', () => {
    beforeEach(() => {
      // setup context
    })
    
    // assertions
    it('should update the state property `item`', () => {
      expect(
        // this.state.item
        wrapper.state().item
      ).toEqual(item)
    })
    
    it('should enable `button`', () => {
      const button = wrapper.find('button').first()
      expect(
        // this.props.disabled
        button.props().disabled
      ).toBe(false)
    })
    
    // Another nested describe()
    describe('and then clears the input', () => {
      beforeEach(() => {
        const input = wrapper.find('input').first()
        input.simulate('change', {
          target: { value: '' }
        })
      })
      
      it('should disable `button`', () => {
        const button = wrapper.find('button').first()
        expect(
          button.props().disabled
        ).toBe(true)
      })
    })
  })
})
```

## Testing React

`react-test-renderer` enables shallow rendering, but it is a bit low-level and can be verbose. **Enzyme** wraps `react-test-renderer` with lots of handy functionality to aid component testing.

```js
// ShallowWrapper provides us with loads of useful methods
// to traverse and select elements on the virtual DOM
const wrapper: ShallowWrapper = Enzyme.shallow(
  <App />
)
```

Shallow rendering:

1. It tests component in isolation - we don't have to worry about child dependencies.
2. It's faster - you avoid the DOM entirely.

Mount rendering:

1. Mount all children, good for interaction testing


