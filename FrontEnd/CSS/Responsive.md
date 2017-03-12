# Responsive

```css
.container {
  width: 90%;
  max-width: 1024px;
  margin: 0 auto;
}

/* Mobile-first with min-width */
/* By default, it is stacked vertically with no float */
@media screen and (min-width: 700px) {
  .sidebar {
    width: 24.4140625%; /* 250/1024 = 0.244140625 */
    float: left;
  }
}
```

## `calc()`

`calc()` is very useful for responsive design when you want to take value away from a percentage value.

## Viewport Units

* [Unexpected power of viewport units in CSS](https://www.lullabot.com/articles/unexpected-power-of-viewport-units-in-css)
* [Viewport unit based typography](https://zellwk.com/blog/viewport-based-typography/)

```css
h1 {
  font-size: calc(100% + 5vw);
}
```

## Media Queries

* [PX, EM or REM Media Queries?](https://zellwk.com/blog/media-query-units/)
* [On container queries](https://ethanmarcotte.com/wrote/on-container-queries/)