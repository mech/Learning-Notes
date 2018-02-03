# Flow

> When working with types, you find yourself asking this question: What is this? If you can identify it, it has a type.

* [Flow guide](https://github.com/ryyppy/flow-guide)
* [Even Better Support for React in Flow 0.53.0](https://medium.com/flow-type/even-better-support-for-react-in-flow-25b0a3485627)
* [Why use static types in JavaScript? (A 4-part primer on static typing with Flow)](https://medium.freecodecamp.org/why-use-static-types-in-javascript-part-1-8382da1e0adb)
* [Make your Flow errors GLOW](https://github.com/thejameskyle/glow)

> Type correctness does not guarantee program correctness. If you haven't exercised the code, you really have no idea whether or not it works.

Types and tests are both great mechanisms for doing "think real hard up front" thinking.

Types are a set of possible values. Types can be strong or generic.

Haskell is perhaps one of the most strongly typed languages. However, Haskell support Generic Programming, in the sense that you write methods that work with any type conforming to a certain concept (or interface). Duck typing! Haskell also uses Type Inference so you never have to declare the type of your variables.

Python and Ruby are strongly typed, dynamic languages. JavaScript is a weakly typed, dynamic language.

> Looking at the code, it's hard to know what a JavaScript promise resolves with.

What's the purpose of type checking?

* After assigning a value to a variable, you're not allowed to change the type. JavaScript lets you do this, but it's a common cause of de-optimization in modern runtimes (V8's Ignition and TurboFan)
* Let the team knows what types the function needs if you don't write JSDoc (no more `@param` and `@return`).
* Throw type errors if components are not given required props (but leave props with default values as optional)
* Type annotations provide a form of always-up-to-date [documentation](http://documentation.js.org/) for developers to understand unfamiliar code base.
* Provide feedback as you write code
* Designing a type means to understand a domain and its operations
* Keeping a type discipline can be an advantage for long term maintainability
* [Flow is nominal typing](https://flowtype.org/docs/classes.html#structural-vs-nominal-typing-for-classes)
* [TypeScript is structural typing](https://www.typescriptlang.org/docs/handbook/type-compatibility.html)
* [If TypeScript is so great, how come all notable ReactJS projects use Babel?](https://discuss.reactjs.org/t/if-typescript-is-so-great-how-come-all-notable-reactjs-projects-use-babel/4887)
* [Typed Redux](https://blog.callstack.io/typed-redux-2aa8bff926ff)

---

* [The Shocking Secret About Static Types](https://medium.com/javascript-scene/the-shocking-secret-about-static-types-514d39bf30a3)
* [Type systems will make you a better JavaScript programmer](http://jaredforsyth.com/type-systems-js-dev/#/)
* [Advanced features in Flow](http://sitr.us/2015/05/31/advanced-features-in-flow.html)
* [Flow-type cheat sheet](http://www.saltycrane.com/blog/2016/06/flow-type-cheat-sheet/)
* [Why use flow?](https://blog.aria.ai/post/why-use-flow/)
* [dom.js](https://carousell.com/p/genuine-windows-10-pro-95810506/?ref=search&ref_query=windows%2010&ref_rank=14&ref_referrer=%2Fsearch%2Fproducts%3Fquery%3Dwindows%252010)

```
▶ npm install -g flow-bin
▶ npm install -g flow-typed

▶ yarn add global flow-bin
▶ yarn add global flow-typed
▶ flow-typed install

// Not needed anymore as babel-preset-react will strip flow for us
▶ npm install --save-dev babel-plugin-transform-flow-strip-types

// Create .flowconfig file
▶ flow init

▶ yarn flow -- init
```

Flow want annotation on:

* Declarations
* Function parameters

```js
// Just a simple variable binding
var foo = "Hello";
// Variable binding with type annotation
var foo: string = "Hello";

// Type parameters for generic functions
function reversed<T>(array: T[]): T[] {
}

// Custom properties
let rating: {[id:string]: number} = {};
rating["stars"] = 5

// A promise that resolves/returns an array of numbers
Promise<number[]>

Promise<string>
Promise.resolve('hello')

// A promise that returns an array of strings
Promise<string[]>
Promise<string>

Generator<number, void, void>

// Use sparingly
var anyObject: Object = {};
var anyFunction: Function = () => {};

// Structurally similar
interface Fooable {
  foo(): string;
}

// Is Array being defined by Generics type alias?
type Array<T> = [ item: T ];
var stringArray: Array<string> = ['hi', 'there'];

// Same
var array: number[] = [];
var array: Array<number> = [];

// Allowed literal values
const value: 'enabled' | 'disabled' = 'enabled'

// Type unions
const stringOrNumber: string | number = 'foo'

// Object
const obj: { [key: string]: number } = { "foo": 1 }

// Algebraic data type
// AppState type can be one of two types:
type AppState = ViewingState | EditingState;
type ViewingState = { mode: 'Viewing' };
type EditingState = {
  mode: 'Editing';
  articleId: number;
};

class AppComponent extends React.Component {
  // Same as:
  // state: AppState = States.Viewing()
  state: AppState;
  
  constructor(props: any, children: any) {
    this.state = States.Viewing();
  }
  
  // A shim to attach flow annotations and enforce type safety
  setState(object: AppState) {
    super.setState(object);
  }
}
```

```js
// You wouldn't want to write such checking code
function greet(greeting, months, age) {
  if (arguments.length !== 3)
    throw new Error('must be called with 3 arguments')
  if (typeof greeting !== 'string')
    throw new Error('greeting must be a string')
  if (!Array.isArray(months))
    throw new Error('months must be an array')
  if (typeof age !== 'number')
    throw new Error('age must be a number')
}

// Much better with Flow
function greet(greeting: string,
               months: Array<string>,
               age: number) {
}
```

* If it is hard to type check, it is probably hard to understand

```js
function isValid(items: Array<string>): boolean {
}
```

## .flowconfig

```
[ignore]
.*/node_modules/stylelint/.*
<PROJECT_ROOT>/node_modules/styled-components/*

[include]

[libs]
styled-components

[options]
```

## Any Type



## Type Aliases

Make it easy to refer to complex type by simple name. Essential to sharing codebase.

```js
import type { MediaType } from './MediaType'

export type UserType = {
  username: string,
  firstName?: string,
  lastName?: string,
  email: string,
  avatar: MediaType,
}

// Create a Dictionary type alias. This will allow us to
// define data that follows the { key: value } model shape
type Dictionary<K, T> = {[key: K]: T};

{
  tracks: Dictionary<Track, number>
}
```

## Object Types

```js
type Person = {
  name: string,
  age: number,
  (x: string): number, // callable property
  [x: number]: string  // computed property
}
```

**Exact Object Types**

```js
type ObjType = {|
  value?: string
|}
```

## Function Types

```js
type TimesTwo = (value: number) => number;

// Type parameter for generic function type
type Identity = <T>(x: T) => T;
```

Function types is good for writing callbacks:

```js
function method(callback: (error: Error | null, value: string | null) => void) {
}
```

## Tuples

Tuple is an array that use positional items like `["foo", 1, true]`.

```js
const tuple: [string, number, boolean] = ["foo", 1, true];
```

## Polymorphic Types

* [Flow: Mapping an object](https://medium.com/@thejameskyle/flow-mapping-an-object-373d64c44592#.7n0tsa306)

Really sound scary, but are actually much more simple than they sound.

## Generic and Type Parameters

When you write code that doesn't care about types, you can use generics which are kind of like type placeholders.

`T` is often used as a type that will be defined at the call-site. `T` is a type template representing a substitution variable. `T` can be a boolean, a number or a type you define or it can be an `interface`.

```js
// `T` here, is a type that will defined at the call-site
// This is a "generic function"
function findLast<T>(
  array: Array<T>,
  func: (item: T, index: number, array: Array<T>) => any
): null | T {
  let index = array.length
  while(--index >= 0) {
    const item = array[index]
    if(func(item, index, array)) {
      return item
    }
  }
  return null
}

// Flow knows that in this case, `T` will be a number
const lastEvenNumber: ?number = findLast(
  [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ],
  (item) => item % 2 === 0
)
```

```js
// Type parameters - Looks like React's props and state
class GenericClass<T> {
  x: T;
  
  constructor(x: T) {
    this.x = x;
  }
}
```

```js
// If you find yourself using `any` for generic type
function first(arr: any[], predicate: (x) => boolean): any {
}

// You can change it to a generic function
function first<T>(arr: T[], predicate: (x: T) => boolean): T {
}

// So why do we do this? So that IDE can show us available methods to use
var arr = [4, 16, 7, 21]
var item = first(arr, x => !!(x % 2))
item. // => here we have intellisense
```

```js
// Promise is a parameterized type??
// what this promise resolve is an object containing a
// `default` property which is a Class type
props: {
  props: mixed,
  loadingPromise: Promise<{ default: Class<React.Component<*, *, *>> }>
}
```

## Type-First Approach

```js
// Type alias
type Post {
  title: string,
  createdAt: Date,
  contents: string,
  authors: Array<{
    name: string,
    location: string,
    numberOfPosts: number
  }>
}

type Kibble = Array<any> | number

// Simple type aliases
type Username = string
type ID = number
type URL = string

type Item = {
  by: Username,
  id: ID,
  time: number,
}

// Intersection type
type Item =
  | { type: 'story', url: URL } & TopLevel
  | { type: 'ask', text: string } & TopLevel
```

```js
declare type ActionSendInquiry = {
  type: 'SEND_INQUIRY';
  action: PetAction;
  id: number;
  inquiry: PetInquiry;
}

declare type SendInquiry = (x: ActionSendInquiry) => void
```

## React

* [Flow Cookbook: Flow & React](http://sitr.us/2017/01/03/flow-cookbook-react.html)

`React.Component` takes type parameters. See [flowtype for react](https://github.com/facebook/flow/blob/master/lib/react.js)

Flowtype annotations provide an alternative to `propTypes` runtime checks. It has the benefit to check `state` as well as `props`.

```js
// New since 0.53.0
type Props = {
  foo: number
}

type State = {
  bar: number
}

class MyComponent extends React.Component<Props, State> {
  // You don't need to provide Flow with any type annotations
  // for default props
  static defaultProps = {
    foo: 42
  }
}

// The same for functional component
function MyComponent({ foo }: { foo: number }) {
  return this.props.foo
}

MyComponent.defaultProps = {
  foo: 42
}
```

```js
type Props = {}
type State = {}
type DefaultProps = {}

// But why do we do these type annotation?
// Flow requires type annotations for class method arguments and return values, so that Flow can:
// 1. Check you're instantiating with the required props
// 2. Props that are not required have default values
// 3. Make sure properties exist for props and state
// 4. Make sure setState() is using declared types
class Counter extends React.Component<DefaultProps, Props, State> {
  constructor(props: Props, context: any) {
    super(props, context)
  }
  
  render(): React.Element<*> {
  }
}
```

```js
// For stateless functional component
function MyComponent(props: Props): React.Element<*> {
}
```

```js
type ModalProps = {
  sendInquiry: SendInquiry;
  pet: Pet;
}

type ModalState = {
  inquiry: ?PetInquiry;
}

class PetModal extends React.Component {
  // This is class field which is specified inside the class
  // body. See "class properties proposal" at stage-2
  props: ModalProps;
  state: ModalState;
  onSubmit: () => void;
  
  constructor(props: ModalProps) {
    super(props);
    
    this.state = {
      inquiry: null
    }
    
    this.onSubmit = () => {
      props.sendInquiry({
        type: 'SEND_INQUIRY',
        action: props.pet.action || 'adopt',
        id: props.pet.id,
        inquiry: this.state.inquiry
      })
    }
  }
}
```

```js
import React, { Component, PropTypes } from "react";
import { connect } from "react-redux";
import { mapDispatchToProps } from "./actions/mappers";

type CurrentArticle = {
  content: string,
  id: number,
  name: string,
};

class ArticleContent extends Component {
  props: {
    category_id: number,
    current_article: CurrentArticle,
    editing: bool,
    saveEditing: (id: number, cat_id: number, name: string) => void,
    startEditing: (id: number) => void,
  };

  state: {
    content_value: string;
  };

  defaultProps: { visited: boolean };

  constructor(props) {
    super(props);
    (this:any).isNotChanged = this.isNotChanged.bind(this);
    (this:any).onChangeContent = this.onChangeContent.bind(this);
    (this:any).onModify = this.onModify.bind(this);
    (this:any).onSave = this.onSave.bind(this);
    (this:any).onUndo = this.onUndo.bind(this);
    (this:any).dangerous = this.dangerous.bind(this);
    (this:any).state = {
      content_value: props.current_article.content
    };
  }
}
```

```js
import type { Story } from 'hacker-news'

// This is type for props
// `onSelect` is a function that takes zero arguments and returns `undefined`
// You can use `mixed` also if you do not want to put any constraint on the callback's return type
type StoryListItemProps = {
  story: Story,
  onSelect: () => void,
}

function StoryListItem(props: StoryListItemProps): React.Element<*> {
  const { by, title } = props.story
  
  return (
    <p>
      <a href="#" onClick={event => selectStory(props, event)}>
      </a> posted by {by}
    </p>
  )
}

function selectStory(props: StoryListItemProps, event: Event) {
  event.preventDefault()
  props.onSelect()
}
```

```js
// mixed is same as any but more safe
type Props = {
  value: string,
  onChange: (value: string) => mixed
}

type State = {
  count: number
}

class MyComponent extend React.Component {
  props: Props
  state: State = { count: 0 }
  
  render() {
  }
}
```

## Disjoint Union

```js
// "leaf" and "branch" are Singleton Types
type BinaryTree =
  { kind: "leaf", value: number } |
  { kind: "branch", left: BinaryTree, right: BinaryTree }
  
function sumLeaves(tree: BinaryTree): number {
  switch (tree.kind) {
    case "leaf":
      return tree.value;
    default
      return sumLeaves(tree.left) + sumLeaves(tree.right);
  }
}
```

## Singleton Types

## Optional

```js
// Optional parameter with trailing ?
function foo(x?) {...}

// Callback is optional, but if defined, take no argument and return nothing
function foo(x: number, callback?: () => void): void {...}
```

## Nullability

Flow has null, but treat it as a distinct type that is generally not compatible with other types. Values are non-nullable by default.

```js
function LoginForm(props) {
  // emailInput might be null
  let emailInput: ?HTMLInputElement
  
  return (
    <form onSubmit={event => props.onLogin(event, emailInput)}>
      <input type="email" ref={el => emailInput = el} />
      <input type="submit" />
    </form>
  )
}

function onLoginTake1(event: Event, emailInput: ?HTMLInputElement) {
  event.preventDefault()
  
  // Type error! Cannot read property `value` on possibly `null` or `undefined` value
  dispatch(loginEvent(emailInput.value))
}

function onLoginTake2(event: Event, emailInput: ?HTMLInputElement) {
  event.preventDefault()
  
  if (emailInput) {
    // Safe! Flow infers that emailInput cannot be `null` or `undefined` in the block
    dispatch(loginEvent(emailInput.value))
  }
}
```

Contrast this to Go's approach:

```go
func validate(user *User) bool {
  return user.Name != ""
}
```

```js
handleSearchTermChange = (evt: SyntheticKeyboardEvent & { target: HTMLInputElement }) => {
  this.setState({
    searchTerm: evt.target.value
  })
}
```

## Variants

* Covariance - Read only
* Contravariance - Write only
* Invariance - Read/Write

## People

* [Jesse Hallett](http://sitr.us/)
* [Giulio Canti](https://medium.com/@gcanti)

## Videos

* [@Scale 2014 - Flow introduced](https://www.youtube.com/watch?v=M8x0bc81smU)

