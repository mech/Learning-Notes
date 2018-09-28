# React Performance

> Poor design choices often lead to issues and, in the case of React, if we do not put the state in the right place, the risk is that our components are going to render more than needed.

* [Debugging React performance with React 16 and Chrome Devtools](https://building.calibreapp.com/debugging-react-performance-with-react-16-and-chrome-devtools-c90698a522ad)
* [React is Slow, React is Fast: Optimizing React Apps in Practice](https://medium.com/dailyjs/react-is-slow-react-is-fast-optimizing-react-apps-in-practice-394176a11fba)
* [Rearchitecting Airbnb's Frontend](https://medium.com/airbnb-engineering/rearchitecting-airbnbs-frontend-5e213efc24d2)
* [React Performance Tune-up](http://engineering.invisionapp.com/post/react-performance-tune-up/)
* [Be careful with code splitting using link preload](https://medium.com/reloading/a-link-rel-preload-analysis-from-the-chrome-data-saver-team-5edf54b08715#.ssqki3op6)
* [High Performance React: 3 New Tools to Speed Up Your Apps](https://medium.freecodecamp.org/make-react-fast-again-tools-and-techniques-for-speeding-up-your-react-app-7ad39d3c1b82)
* [Netflix - Crafting a high-performance TV user interface using React](https://medium.com/netflix-techblog/crafting-a-high-performance-tv-user-interface-using-react-3350e5a6ad3b)
* [Optimizing the Performance of Your React Application](https://auth0.com/blog/optimizing-react/)
* [React at 60fps](https://hackernoon.com/react-at-60fps-4e36b8189a4c)
* [Performance Problems and Solutions in React.js Part 1](https://blog.axosoft.com/2017/03/30/performance-solutions-react-js-pt-1/)
* [A Deep Dive into React Perf Debugging](http://benchling.engineering/deep-dive-react-perf-debugging/)
* [Twitter Lite and High Performance React Progressive Web Apps at Scale](https://medium.com/@paularmstrong/twitter-lite-and-high-performance-react-progressive-web-apps-at-scale-d28a00e780a3)
* [**React at Light Speed**](https://blog.vixlet.com/react-at-light-speed-78cd172a6411)
* [45% Faster React Functional Components, Now](https://medium.com/missive-app/45-faster-react-functional-components-now-3509a668e69f)
* [How to Benchmark React Components: The Quick and Dirty Guide](https://engineering.musefind.com/how-to-benchmark-react-components-the-quick-and-dirty-guide-f595baf1014c)
* [Performance optimisations for React applications](https://medium.com/@alexandereardon/performance-optimisations-for-react-applications-b453c597b191)
* [Normalised state and connected components](https://medium.com/@alexandereardon/performance-optimisations-for-react-applications-round-2-2042e5c9af97)
* [Two Tips to Improve Performance by 30% With React and Webpack](http://engineering.teacherspayteachers.com/2017/08/16/two-tips-to-improve-performance-by-30-with-react-and-webpack.html)

```
http://localhost:3000?react_perf
```

```js
componentWillUpdate() {
  Perf.start()
}

componentDidUpdate() {
  Perf.stop()
  
  // See which operations React has made on the DOM like
  // "insert child"
  Perf.printOperations()
}
```

`PureComponent` should be used only after the application has been monitored and the bottleneck has been found.

```js
class List extends React.Component {
  render() {
    return (
      <ul>
        {this.state.items.map(item => (
          <Item key={item.id} item={item} />
        ))}
      </ul>
    )
  }
}

// Instead of rendering the <li> directly on the parent, we
// create additional component which is "pure" in order to
// take advantage of not rendering any unchanged item.
//
// If we were to just use <li>, it lack any shouldComponentUpdate
// capability and will always re-render.
class Item extends React.PureComponent {
  render() {
    return (
      <li>{this.props.item}</li>
    )
  }
}
```

Don't forget to avoid the common mistakes that make the `PureComponent` less effective, such as generating new functions inside the `render()`, or using constant as props.

## Profiler

* [Profiler RFC #51](https://github.com/reactjs/rfcs/pull/51)
* [Interaction tracking with React](https://gist.github.com/bvaughn/8de925562903afd2e7a12554adcdda16)

## render()

* Do as little work as possible in the `render()` function
* Function binding and Object/Array literals are bad for performance
* Make checks cheap - Invalidate references whenever you change data.
* Make checks easy - Denormalize your data??

## shouldComponentUpdate

> We have a number of high level components that are responsible for fetching data. Whenever new data is fetched, it triggers a render of all of its children. Rendering all children due to a single piece of data updating can be costly and unnecessary when the fetched data doesn't modify the layout. Fortunately, with a couple of strategically placed `shouldComponentUpdate`s we were able to reduce the amount of time spent in scripting, layout, and painting considerably.

We can tell React to avoid reconciling **some parts of the tree**.

To find out the necessary steps to reduce the DOM operations, React has to fire the render methods of all the components and compare the results with the previous ones.

If nothing changes, no changes will be made in the DOM, which is great. But if our render methods do complex operations, React will take some time to figure out that no operations have to be done, which is not optimal.

We surely want our components to be simple and we should avoid doing expensive operations inside the renderer. However, sometimes we simply cannot manage this and our applications become slow, even if the DOM is not touched at all.

React is not able to figure out which components do not need to be updated but we have a function that we can implement to tell the library when to update a component or not.

## Stateless Functional Components

You can still use stateless components if you implement `shouldComponentUpdate()` on your container component correctly to prevent rendering of their children.

It is beneficial to implement `shouldComponentUpdate()` as high up the tree as possible.

## PureComponent

* [Using a `<PureComponent/>` in React](https://medium.com/front-end-hacking/using-a-purecomponent-in-reacts-262972f9f1e0)
* [React Pattern: Extract Child Components to Avoid Binding](https://medium.freecodecamp.org/react-pattern-extract-child-components-to-avoid-binding-e3ad8310725e)
* [Remember to not pass arrow function](https://medium.com/@housecor/hi-dana-great-question-note-this-affbe4a2f168)
* [When to use Component or PureComponent](https://codeburst.io/when-to-use-component-or-purecomponent-a60cfad01a81)
* [Is PureComponent faulty?](https://medium.com/myheritage-engineering/how-to-greatly-improve-your-react-app-performance-e70f7cbbb5f6)
* [Always cache your object before using PureComponent](https://hackernoon.com/react-purecomponent-considered-harmful-8155b5c1d4bc)

Typically you will want to use `PureComponent` for your leaf node in your render tree.

See this [Issue #8669](https://github.com/facebook/react/issues/8669)

## Binding

```js
// Instead of this, which will cause re-render everytime
<CommentItem likeComment={() => this.likeComment(user.id)} />

// Do this
<CommentItem likeComment={this.likeComment} userID={user.id} />

// And use
this.props.likeComment(this.props.userID)
```

## Constant Props

```js
// Will always re-render because props is array literal and
// re-create on every render
render() {
  <Item
    statuses={['open', 'close']}
  />
}

// Instead we should do it outside the render()
const statuses = ['open', 'close']
...
render() {
  <Item
    statuses={statuses}
  />
}
```

## Reselect

* [memoize-one](https://github.com/alexreardon/memoize-one)

## Recompose

* [How to add state to functional components using recompose](http://blog.jakoblind.no/2017/04/03/how-to-add-state-to-functional-components-using-recompose/)
* [Optimizing React Performance with Stateless Components](https://www.sitepoint.com/optimizing-react-performance-stateless-components/)

Functional components can't use `shouldComponentUpdate`.

```js
import pure from 'recompose/pure'
import onlyUpdateForKeys from 'recompose/onlyUpdateForKeys'

const DatagridBody = ({ ids }) => (
  <tbody>
    {ids.map(id => (
      <tr></tr>
    ))}
  </tbody>
)

export default pure(DatagridBody)
```

## react-fast-compare

* [react-fast-compare](https://github.com/FormidableLabs/react-fast-compare)

First, see if a `PureComponent` would work for you. If it won't and you need deep checks, then use this.

## Server-Side Rendering

* [Using Electrode to Improve React Server Side Render Performance By Up To 70%](https://medium.com/walmartlabs/using-electrode-to-improve-react-server-side-render-performance-by-up-to-70-e43f9494eb8b)

## Videos

* [Performance optimisations for React: round 3](https://www.youtube.com/watch?v=JZF06CPqOQ0)
* [Scaling My First Enterprise React App!](https://www.youtube.com/watch?v=sL4D_zRUVw4)

