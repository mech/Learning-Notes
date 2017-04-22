# Flexbox

* [How To Approach CSS layouts in 2017 — and beyond](https://medium.com/flexbox-and-grids/css-flexbox-grid-layout-how-to-approach-css-layouts-in-2017-and-beyond-685deef03e6c)

Traditionally, we have 3 ways to do layout:

1. `float` - Need clearfix hack
2. `display: inline-block` - whitespace sensitive
3. `display: table` - `border-spacing`

```css
/* With Modernizr, we can have fallback */
.wrapper {
  width: 600px;
  margin: 0 auto;
}

.card {
  display: inline-block;
  vertical-align: top;
}

.flexbox .wrapper {
  display: flex;
  flex-wrap: wrap;
}
```

---

* [Understanding Flexbox: Everything you need to know](https://medium.freecodecamp.com/understanding-flexbox-everything-you-need-to-know-b4013d4dc9af#.44b5tgfom)
* [The Ultimate Flexbox Cheat Sheet](http://www.sketchingwithcss.com/samplechapter/cheatsheet.html)
* [Codrops' Flexbox Reference](https://tympanus.net/codrops/css_reference/flexbox/)
* [Flex-grow 9999 Hack](http://joren.co/flex-grow-9999-hack/)
* [flex-grow is weird. Or is it?](https://css-tricks.com/flex-grow-is-weird/)
* [How Flexbox works - explained with big, colorful, animated gifs](https://medium.freecodecamp.com/an-animated-guide-to-flexbox-d280cf6afc35#.3jg4somu6)
* [Even more about how Flexbox works - explained in big, colorful, animated gifs](https://medium.freecodecamp.com/even-more-about-how-flexbox-works-explained-in-big-colorful-animated-gifs-a5a74812b053#.kd8xsu86o)
* [Flexbox is awesome but don't use it here](https://medium.com/@ohansemmanuel/flexbox-is-awesome-but-its-not-welcome-here-a90601c292b6#.7m0yqvvqc)
* [In CSS Flexbox, why are there no `justify-items` and `justify-self` properties?](https://stackoverflow.com/questions/32551291/in-css-flexbox-why-are-there-no-justify-items-and-justify-self-properties)

Using float is like pre-defining the width of your element. It is not very content focus and is very width focus.

> Flexbox is an efficient way to align and distribute space for dynamic items in a container along an axis.

* Distribute space among flex-items. Expand and grow to fill unused space or shrink items to prevent overflow the parent.
* Flexbox is all about alignment and ordering. It is a smart layout mode that calculates and distributes space.
* Don't always think you need to use media queries. Most of the time a default flexbox can make the site very responsive already.
* Flexbox lets the DOM know that elements on the page have a relationship
* Don't force flexbox to be a grid system, it was not designed for that!
* Flexbox will override floats, table-cell and inline-block. It will not override absolute positioning.
* <strong style="color:red;">Don't use flexbox as a true Grid System, even if you can get away with it</strong>
* Use flexbox for progressive enhancement only and fallback to table display

To understand why flexbox is not meant for grid system, you can imagine a layout like the [Pricing Example](https://thecssworkshop.com/lessons/a-flexbox-pricing-example) where 3 boxes of pricing with uneven bottom content with multiple lines.

## Browser Support

* IE9, Opera 12 don't support flexbox
* IE10 has tweener flexbox
* IE10-IE11, flex-items ignore their parent container's height if it's set via the `min-height` property.

## Flex Container

Establishes a **flexbox-formatting context** in contrast to block-formatting context. A flex container expands items to fill available space, or shrinks them to prevent overflow.

A couple of alignment properties are made available to be used on the flex-container:

```
flex-direction: row | column | row-reverse | column-reverse
flex-wrap: wrap | nowrap | wrap-reverse
flex-flow: flex-direction flex-wrap
justify-content: flex-start | flex-end | center | space-between | space-around
align-items: flex-start | flex-end | center | stretch | baseline
align-content: flex-start | flex-end | center | stretch
```

* `justify-content` defines how flex-items are laid out on the **main axis**. For `row`, the main axis is horizontal, for `column`, it is vertical.
* `align-items` defines how flex-items are laid out on the **cross axis**.
* `align-content` is very interesting and only happen if flex-items wrap to become multi-line.

Note that for `align-items: stretch`, you had to set `height: auto` or else the height property would override the stretch.

## Flex Items

The children of flex-item do not become flex-item automatically. It is only one level deep. Only direct children of a flex container become flex items, not its descendants.

```
order: 0 | -ve | +ve
flex-grow: 0 | +ve
flex-shrink: 1 | +ve
flex-basis: auto | percentages | ems | rems | pixels
flex: flex-grow flex-shrink flex-basis
align-self: auto | flex-start | flex-end | center | baseline | stretch
```

By default, flex-item does not grow to fit the entire space available. It's `flow-grow: 0` which turns off this growth.

`flex-basis` default value is `auto` which has the width of its content area.

```css
/* Absolute flex because flex-basis is 0 */
/* All flex-item will have the same width */
flex: 1 1;
flex: 1;

/* Default behavior for all flex-items */
/* I will not grow, but I will shrink. I maintain an auto width */
flex: 0 1 auto;
flex: initial;

/* Item does not grow or shrink, essentially a fixed width element */
flex: 0 0 auto;
flex: none;

/* Grow to fit the entire space and shrink if necessary */
flex: 1 1 auto;
flex: auto;

/* No width, grow the item to fill available space and shrink if needed */
/* The widths of the flex-items are computed based on the ratios of the flex-grow value */
flex: 2 1 0;
flex: 2;
```

* `align-self` align a **single** flex-item along the cross-axis (vertical by default). It basically overriding `align-items` for one item.

## flow-grow

flow-grow will take the remaining space and divide it by the total amount of flex grow values.

If an element has `flex-grow` set to 3 it does not mean that it's 3 times bigger than an element that has `flex-grow` set to 1, but it means that it gets 3 times more pixels added to its initial width than the other element.

flow-grow will override its `width` if necessary.

The math involved in calculating the remaining space is as follow: add all the `flex-grow` and divide it the available remaining space after `flex-basis` is applied. Do not divide it by the parent container's width.

## flow-basis

`flex-basis` controls how large an element will be along the main-axis **before** any growing or shrinking occurs.

Set `flex-basis: auto` and give it a `width`. If you don't supply a `width`, then `auto` become the **content width**.

```css
/* All item with equal width, we don't want to set to auto which is content width */
.option {
  flex: 1 1 0;
}
```

## Auto Margin

Auto margin is useful together with flexbox.

```css
li:last-child {
  margin: 0 0 0 auto;
}
```

If you use `margin: auto` alignment on flex-item, the `justify-content` property no longer works.

## Bugs, Advice

* [Flexbugs by Philip Walton](https://github.com/philipwalton/flexbugs)

Whenever building a layout in flexbox, you should start by looking out for what sections of your layout may stand out as flex-containers.

* Be careful when you mark `body` as `display: flex`, it will screw up all your block-level elements and make them unable to become 100% full-width since you are essentially marking all immediately children as flex items.

## Examples

```html
<!-- Footer stick to the bottom -->
<main></main>
<footer></footer>

<style>
main {
  /* Please compute the size of the flex item automatically, but never shrink */
  flex: 1 0 auto;
}

footer {
  /* 100px here refer to the height, since flex-direction is column */
  flex: 0 0 100px;
}
</style>
```


## Video

* [It's Time To Ditch The Grid System](https://www.youtube.com/watch?v=5N9RkIs31Ok)
* [CSS4 Grid: True Layout Finally Arrives](https://www.youtube.com/watch?v=jl164y-Vb5E)