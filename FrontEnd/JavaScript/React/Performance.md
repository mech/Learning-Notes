# React Performance

* [React Performance Tune-up](http://engineering.invisionapp.com/post/react-performance-tune-up/)
* [Be careful with code splitting using link preload](https://medium.com/reloading/a-link-rel-preload-analysis-from-the-chrome-data-saver-team-5edf54b08715#.ssqki3op6)
* [High Performance React: 3 New Tools to Speed Up Your Apps](https://medium.freecodecamp.org/make-react-fast-again-tools-and-techniques-for-speeding-up-your-react-app-7ad39d3c1b82)
* [Netflix - Crafting a high-performance TV user interface using React](https://medium.com/netflix-techblog/crafting-a-high-performance-tv-user-interface-using-react-3350e5a6ad3b)
* [Optimizing the Performance of Your React Application](https://auth0.com/blog/optimizing-react/)
* [React is Slow, React is Fast: Optimizing React Apps in Practice](https://marmelab.com/blog/2017/02/06/react-is-slow-react-is-fast.html)
* [React at 60fps](https://hackernoon.com/react-at-60fps-4e36b8189a4c)

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

## Recompose

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