# React Form

* [**Introducing Formik 0.9.0**](https://medium.com/@jaredpalmer/introducing-formik-0-9-0-690959a329a6)
* [Govern - good state management for form?](https://github.com/jamesknelson/govern)

Creating a rich, interactive, easy to use form can often involve a **significant amount of programming**.

> Thinking in React apply to form also: It's best not to think in terms of "getting data from a form or user input". You get your data from your "state".

Form components are always stateful:

```js
class TimerForm extends Component {
  state = {
    title: this.props.title || '',
    project: this.props.project || ''
  }
} 
```

```js
// Always separate business logic from event
handleCreateFormSubmit = (timer) => {
  // We may want to call newTimer() elsewhere
  Timer.newTimer(timer)
}
```

* [A list of form drivers](https://github.com/markerikson/redux-ecosystem-links/blob/master/forms.md)
* [**Formik**](https://github.com/jaredpalmer/formik)
* [**React Final Form**](https://github.com/final-form/react-final-form)
* [NeoForm](https://github.com/zero-plus-x/neoform)
* [React.js controlled components](http://blog.klipse.tech/react/2016/12/20/react-controlled-components.html)
* [Form Validation as HOC](https://medium.com/javascript-inside/form-validation-as-a-higher-order-component-pt-1-83ac8fd6c1f0#.fv2zg6miy)
* [react-reform](https://github.com/codecks-io/react-reform)
* [react-jsonschema-form](https://github.com/mozilla-services/react-jsonschema-form)
* [Web Form Validation: Best Practices](https://www.smashingmagazine.com/2009/07/web-form-validation-best-practices-and-tutorials/)
* [How to create a Redux-Form with validation and initialized values](https://www.davidmeents.com/blog/create-redux-form-validation-initialized-values/)
* [Form Validation Example With React](https://stvmlbrn.github.io/2017/01/16/form-validation-with-react.html)
* [Submitting Form Data With React](https://stvmlbrn.github.io/2017/04/07/submitting-form-data-with-react.html)
* [Native form validation — part 1](https://medium.com/samsung-internet-dev/native-form-validation-part-1-bf8e35099f1d)
* [revalidation - HOC for validating forms](https://github.com/25th-floor/revalidation)
* [Writing a Wizard in React](https://medium.com/@l_e/writing-a-wizard-in-react-8dafbce6db07)

```js
// Generic change handler
handleChange({ target }) {
  this.setState({
    [target.name]: target.value
  })
}

// At the form
<form onChange={this.handleChange}>
```

```js
const AddTodo = ({onAddClick}) => {
  let input
  
  return (
    <div>
      <input ref={node => input = node} />
      <button onClick={() => {
        onAddClick(input.value)
        input.value = ''
      }}>
        Add Todo
      </button>
    </div>
  )
}
```

What API is good for inputs:

```js
<Form onSubmit={this.handleSubmit}>
  <Text name="email" label="Email" isRequired isEmail />
  <Password name="password" label="Password" isRequired />
</Form>
```

## File API

* [File API - MDN](https://developer.mozilla.org/en-US/docs/Web/API/File)
* [Using files from web applications](https://developer.mozilla.org/en-US/docs/Web/API/File/Using_files_from_web_applications)

## Show Errors

`null` can be a good way to show error messages

```js
function InputErrorMessage({ message }) {
  if (!message) {
    return null;
  }
  
  return (
    <div className="field-error">
      {message}
    </div>
  )
}

class MyForm extends Component {
  render() {
    <FormGroup>
      <TextInput name="Email" />
      <InputErrorMessage message={this.state.email_error} />
    </FormGroup>
  }
}
```

## Formik

* [Formik For React: A Dive Into Field Arrays](https://medium.com/@rossbulat/react-formik-a-dive-into-field-arrays-fc58fff8a791)

## No Framework

Most of the time, form should be simple to do and no framework like Formik is required.

```js
// Make use of dataset for passing ID
handleIndexClick = event => {
  this.setState({
    active: +event.target.dataset.index
  })
}

render() {
  <img
    src={photo.value}
    onClick={this.handleIndexClick}
    data-index={index}
    className={index === active ? 'active' : ''}
  />
}
```

## Input Mask

* [**JavaScript Events Unmasked: How to Create an Input Mask for Mobile**](https://medium.com/outsystems-experts/javascript-events-unmasked-how-to-create-an-input-mask-for-mobile-fc0df165e8b2)
* [Text Input Mask for React Native](https://blog.cloudboost.io/text-input-mask-for-react-native-3c04e82843a6)
* [react-number-input-field](https://github.com/mitchallen/react-number-input-field)

## Children, cloneElement, etc.

* [Unravelling the Thought Process — how to rationally explore problems in engineering](https://hackernoon.com/unravelling-the-thought-process-how-to-rationally-explore-problems-in-engineering-ad78fc45bc86)

## Forms as Data - Data IS King

Treating forms as data. React changed the way we think about writing applications. Data is king. The pixels are just a "view" of the data.

Instead of forms being an exception, forms are treated in the way everything else in React is - **Data First**.

Forms felt like a monologue.

> The shared trait among all the cases is that in React, all forms are data. The field values are data. Whether a certain field was touched, or whether a form is being submitted at the moment, is data too.

## `<Form>` Component

## `<Field>` Component

`Fields` and `Input` components are different. A `Field` is a logical abstraction for representing a piece of data.

An `Input` component is a way to see and edit the `Field`.

## Handling Events

> You cannot return `false` to prevent default behavior in React. You must call `preventDefault` explicitly.

* [Events Live Cheatsheet](https://reactarmory.com/resources/react-events-cheatsheet)
* [Best alternative to binding in render()](https://daveceddia.com/react-best-alternative-bind-render/)
* [React Binding Patterns: 5 Approaches for Handling `this`](https://medium.com/@housecor/react-binding-patterns-5-approaches-for-handling-this-92c651b5af56?ref=mybridge.co)
* [Event Switch](https://github.com/chantastic/reactpatterns.com#event-switch)
* [React - to Bind or Not to Bind](https://medium.com/shoutem/react-to-bind-or-not-to-bind-7bf58327e22a)
* [React Pattern: Extract Child Components to Avoid Binding](https://medium.freecodecamp.org/react-pattern-extract-child-components-to-avoid-binding-e3ad8310725e)

Synthetic Events are reusable and there is a single global handler. This means you cannot store a synthetic event and reuse it later because it becomes `null` right after the action. If you really want to store it, you can use `persist()`.

```js
// SyntheticEvent is pooled and reuse and will be reset, so this won't work
handleClick(evt) {
  setTimeout(function() {
    // ERROR - name will be null
    console.log(evt.target.name)
  }, 1000)
}
```

```js
// Note that this returns a function
select(choice) {
  return (evt) => {
    this.setState({
      payMethod: choice
    })
  }
}

// Note our onClick is calling a function first that return a function
// This is common pattern for passing arguments to handlers.
// We close over the choice argument when we call `select`.
render() {
  return (
    <PayPalPaymentChoice
      onClick={this.select('PayPal')}
    />
  )
}
```

```js
// `todos` and `onTodoClick` are promoted to the props because we
// want this to be a presentational component
// BAD - poor performance as it need to re-render whenever props
// changes due to function binding and lack of shouldComponentUpdate
const TodoList = ({
  todos,
  onTodoClick
}) => (
  <ul>
    {todos.map(todo =>
      <Todo
        key={todo.id}
        {...todo}
        onClick={() => onTodoClick(todo.id)}
      />
    )}
  </ul>
)

// At the top-level App
<TodoList
  todos={visibleTodos}
  onTodoClick={id =>
    store.dispatch({
      type: 'TOGGLE_TODO',
      id
    })
  }
/>
```

```js
// Notice that the remove() is passed in as well as id
const Item = ({ id, title, remove }) => (
  <div className="item">
    {title}
    <span
      className="deleteItem"
      onClick={() => remove(id)}
    >Delete</span>
  </div>
)
```

These are 2 **BAD** ways to do binding in component, because it will cause Component to re-render as different reference has been passed every time:

* `<Component onClick={() => this.handleClick()} />`
* `<Component onClick={this.handleClick.bind(this)} />`

We need to pre-bind them in the constructor.

## Controlled Components

> Always prefer Controlled Component. Don't let HTML handle its internal state. React should be responsible for it.

* Good for validation
* Good for maintaining form state
* [Controlled / Uncontrolled React Components](https://www.viget.com/articles/controlling-components-react)

```js
state = {
  fields: {
    name: '',
    email: ''
  },
  fieldErrors: {}
}

onInputChange = (evt) => {
  const fields = this.state.fields
  fields[evt.target.name] = evt.target.value
  this.setState({ fields })
}

validate(fields) {
  const errors = {}

  if (!fields.name) errors.name = 'Name Required!'  

  return errors
}

onFormSubmit = (evt) => {
  const fieldErrors = this.validate(this.state.fields)
  this.setState({ fieldErrors })
  
  // Do not proceed if there are errors
  if (Object.keys(fieldErrors).length > 0) return;
}
```

## Refs

Before using refs, see if you can use **Controlled Component** instead.

> Access the underlying DOM node and **component instance**

A way to perform imperative operations on DOM nodes using refs.

We should be careful because refs break some of the conventions that make React easy to work with.

There might be some cases where you need to access the underlying DOM nodes to perform some imperative operations. It should be avoided because, in most cases, there is a more React-compliant solution to achieve the same result, but it is important to know that we have the possibility to do it and to know how it works so that we can make the right decision.

---

Usually an anti-pattern in React, because you should use its declarative way of doing things and its unidirectional data flow.

* [When to use Ref on a DOM node in React](https://www.robinwieruch.de/react-ref-attribute-dom-node/)

In case we need it, React gives us access to the actual DOM nodes in a way that we can perform imperative operations with them (like 3rd-party libraries).

Using refs is imperative (i.e. `input.focus()`) and we should avoid using refs as much as possible because they force the code to be more imperative and harder to read and maintain.

It is important to note that when setting the ref callback on a non-native component, the reference will be the whole instance itself and not the DOM node:

```js
// This does not give us the DOM node instance, rather the custom
// component named Input
<Input ref={element => t(his.element = element)} />

// For stateless component
let input
<input ref={element => input = element} />
```

**Warn**: In general we should avoid using refs because they force the code to be more imperative, and harder to read and maintain.

## Validate in Real-Time

* [Yup - Dead simple Object schema validation](https://github.com/jquense/yup)
* [validator.js - String validation](https://github.com/chriso/validator.js)
* [An Introduction to Validation in React with Yup](https://medium.com/@rossbulat/introduction-to-yup-object-validation-in-react-9863af93dc0e)

How we can validate in real-time at the **field level** and we'll create a `Field` component to improve the maintainability when an app has **multiple fields with different validation requirements**.

It would be ideal if each field was responsible for identifying validation errors on its own input, and the parent form was only responsible for identifying issues at the form-level.

2 different levels of validation:

1. Form level - validate whole models at `onSubmit`
2. Field level - validate in real-time at `onChange`

It is nice to have `<Input isRequired />` field-level validation, but we have to remind ourselves that validation status isn't "local" to fields. If we need to submit the form as a whole, we need to know about form-level validation!

Another nice feature of form level is disabling/enabling the form submit button in real-time as the form passes/fails validation. This is a nice bit of feedback that can improve a form's UX and make it feel more responsive.

```js
<input type="submit" disabled={this.validateForm()} />
```

```js
// Form level component
// For form component to prevent submission, it will need to know
// about field level validation errors
onInputChange = ({ name, value, error }) => {
  const fields = this.state.fields
  const fieldErrors = this.state.fieldErrors
  
  fields[name] = value
  fieldErrors[name] = error
  
  this.setState({ fields, fieldErrors })
}

validateForm() {
  const model = this.state.fields
  const fieldErrors = this.state.fieldErrors
  const errMessages = Object.keys(fieldErrors).filter(k => fieldErrors[k])
  
  if (!model.name) return true
  if (!model.email) return true
  if (errMessages.length > 0) return true
  
  // False means no error, and can proceed to submit form
  return false
}
```

```js
<Field value="from-parent" onChange={} validate={} />

// Can it be PureComponent since it got its value from <Form>
class Field extends PureComponent {
  state = {
    value: this.props.value,
    error: false
  }

  // Because <Form> which is the parent will pass value to us
  // This is also good if <Form> want to clear out field's value
  // like a form reset.
  componentWillReceiveProps(nextProps) {
    this.setState({ value: nextProps.value })
  }
  
  onChange = (evt) => {
    const name = this.props.name
    const value = evt.target.value
    const error = this.props.validate ? this.props.validate(value) : false
    
    this.setState({ value, error })
    
    // We pass back to the <Form>
    // which will pass back us and componentWillReceiveProps
    // will update the render() again
    this.props.onChange({ name, value, error })
  }
}
```

Another way to write validate():

```js
function validate(inputs) {
  return {
    email: inputs.email.length > 3 ? null : 'Email should be longer than 3 characters'
  }
}

// Use it at the render()
// Computing errors in render() is just one approach
// Another approach is keeping the errors in state
render() {
  const errors = validate({
    email: this.state.email
  })
}
```

Generally the submit:

```js
handleSubmit = (evt) => {
  evt.preventDefault()
  
  this.setState({ isSubmitting: true })
  
  const shouldAbort = anyError(this.state.errors)
  if (shouldAbort) {
    return
  }
  
  saveData()
  .then()
}
```

## Debounce

```js
// Add deps
▶ yarn add lodash.debounce

import debounce from 'lodash.debounce'

class SearchInput extends Component {
  state = {
    searchTerm: ''
  }
  
  doSearch = debounce(() => {
    this.props.doSearch(this.state.searchTerm)
  }, 300)
  
  handleSearch = (evt) => {
    this.setState({
      searchTerm: evt.target.value
    }, () => {
      this.doSearch()
    })
  }
}
```

## Libraries

* [formsy-react](https://github.com/christianalfoni/formsy-react)
* [react-input-enhancements](https://alexkuz.github.io/react-input-enhancements/)
* [tcomb-form](https://github.com/gcanti/tcomb-form)
* [winterfell](https://github.com/andrewhathaway/winterfell)
* [react-redux-form](https://github.com/davidkpiano/react-redux-form)
* [Revalidation](http://revalidation.oss.25th-floor.com/)
* [react-final-form-html5-validation](https://github.com/final-form/react-final-form-html5-validation)

## Videos

* [ReactNYC - Formik](https://www.youtube.com/watch?v=-tDy7ds0dag)

