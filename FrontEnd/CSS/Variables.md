# CSS Variables / Custom Properties

By using variables in CSS, you can localize values and simplify initial development, iterative testing, and later maintenance all in one go.

* [CSS Variables — No, really!](https://medium.com/dev-channel/css-variables-no-really-76f8c91bd34e)

```css
/*
 * Declare your variables in the :root pseudo-class selector
 * Since :root matches the whole HTML page, it makes all your
 * variables global in scope.
 */
:root {
  --bg-color: #fff;
}
```

## Scope

```css
section.thisweek {
  --h1-color: red;
}

section.lastweek {
  --h1-color: blue;
}

article h1 {
  color: var(--h1-color);
}
```