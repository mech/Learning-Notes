# TypeScript

https://github.com/paulcbetts/spawn-rx/pull/12/files

* [Product Type and Sum Type](http://blog.jenkster.com/2016/06/functional-mumbo-jumbo-adts.html)
* [TypeScript — JavaScript with superpowers](https://medium.freecodecamp.org/typescript-javascript-with-super-powers-a333b0fcabc9)

## Bivariant and Contravariant

* [What are covariance and contravariance?](https://www.stephanboyer.com/post/132/what-are-covariance-and-contravariance)
* [Covariance and contravariance (computer science)](https://en.m.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science))

## Implicit Typing

* Assignment

## Explicit Typing

* Function parameters
* Function return type

## With React

* [TypeScript loves React](https://medium.com/@basarat/typescript-developers-love-react-9871b494bc1a)
* [Getting started with React.js and Typescript](https://jjude.com/react-with-tsc/)
* [Using React in VS Code](https://code.visualstudio.com/docs/nodejs/reactjs-tutorial)

## Structural vs Nominal

TypeScript is **structural** rather than nominal, meaning that it works basically like automatic duck typing rather than name or identity based type checking. That is a good fit for dynamic languages like JavaScript.

Go uses interfaces and structural typing. Structural typing is like compile-time duck typing.

Structural typing is an alternative to classical inheritance in statically typed languages. It allows you to write generic algorithms without obscuring the definition of a type in a sea of interfaces. It helps statically type languages capture the feel and productivity of dynamically typed languages.

Flow uses structural typing for objects and functions, but nominal typing for classes.

## Interfaces

In addition to classes, we can use interfaces to drive code consistency between domain concepts.

```js
interface HelloProps {
  name: string
}

class Hello extends React.Component<HelloProps, {}> {
  public render() {
    return <div>Hello, {this.props.name}</div>
  }
}
```

## Enums

* Aka Union Types, Sum Types (Algebraic Data Types)
* [Use union type instead of boolean](https://robots.thoughtbot.com/booleans-and-enums)

## Testing

* [Stencil's way of configuring Jest for a TypeScript project](https://stenciljs.com/docs/testing)

