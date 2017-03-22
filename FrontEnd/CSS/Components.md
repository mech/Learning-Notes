# Components

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