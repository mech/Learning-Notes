# CSS Introduction

* [Lesser known CSS quirks & advanced tips](https://medium.com/@peedutuisk/lesser-known-css-quirks-oddities-and-advanced-tips-css-is-awesome-8ee3d16295bb)
* [30 Seconds of CSS](https://30-seconds.github.io/30-seconds-of-css/)
* [CSS and Network Performance](https://csswizardry.com/2018/11/css-and-network-performance/)

## Do

* Use shallow selector 
* Use shorthand properties - See https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties
* Use preload link header: `Link: </css/styles.css>; rel=preload; as=style`
* Use **csscss** tool to find duplicate rules

Use negation instead of using 2 different selectors:

```css
/* Nope */
li { margin-right: 10px; }
li:first-of-type { margin-right: 0; }

/* Yeah */
li:not(:first-of-type) { margin-right: 10px; }
```

## Tips

* [How to create a responsive navigation with Flexbox and CSS Grid and a no JS dropdown](https://www.youtube.com/watch?v=8QKOaTYvYUA)