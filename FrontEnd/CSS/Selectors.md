# Selectors

```css
a[href$=".pdf"] { background-image: url(/i/pdf-icon.svg); }
a[href$=".doc"] { background-image: url(/i/msword-icon.svg); }
a[href^="mailto:"] { background-image: url(/i/email-icon.svg); }
```

## Pseudo Class

```js
document.querySelector('.box:nth-child(2)');
```

### :not()

* [MDN - :not()](https://developer.mozilla.org/en/docs/Web/CSS/:not)

```css
/* A reminder that the content of your :not() selectors contributes toward their specificity */

/* Defined first, but contains a class */
.foo:not(.bar) {
  color: red;
}

/* Defined last, but gets trumped by the previous class */
.foo:not(div) {
  color: green;
}
```

### :any-link

Match `:link` and `:visited`

```css
nav:any-link {
  color: var(--mainColor);
}

/* Will become */
nav:link,
nav:visited {
  color: #aaa;
}
```

### :enter

```css
nav :enter > span {
  background-color: yellow;
}
```

