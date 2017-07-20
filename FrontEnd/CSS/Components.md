# Components

* https://github.com/primer/primer-forms/blob/master/lib/form-control.scss
* [Complete Guide to CSS](https://webdesign.tutsplus.com/series/learn-css-the-complete-guide--cms-1065)

## Examples

```js
<AppBar
  title="Title"
  iconElementLeft={<IconButton><Close /></IconButton>}
  iconElementRight={this.state.logged ? <Logged /> : <Login />}
/>
```

## Button

* [The ins and outs of input](https://www.youtube.com/watch?v=T1OwKW3tokE)

`button` don't work as flex-container. Use a wrapper element that can be a flex-container like `div` or `span` directly inside of `button`.

```html
<button>
  <span>
    <svg></svg>
    <span>Home</span>
  </span>
</button>
```

## Menu

Use checkbox hack to open and close the menu so we don't need to wait for JavaScript to load to do that.

```css
.menu {
  transform: translateX(-500px);
}

.toggle:checked ~ .menu {
  transform: none;
}
```

## Tabs

```js
handleTabClick(selectedTab) {
  this.setState({ selectedTab })
  
  // Let parent know that UI has changed
  this.props.tabEvents.onClick(selectedTab)
}

renderTabContent(isOverview) {
  const currentTab = this.state.selectedTab
  const tab = _.find(this.props.tabs, { key: currentTab })
  const tabContent = tab.content
  
  return _.isFunction(tabContent) ? tabContent() : tabContent
}
```