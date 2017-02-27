# Components

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