# React Performance

* [React Performance Tune-up](http://engineering.invisionapp.com/post/react-performance-tune-up/)

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