# Flexbox

* [Understanding Flexbox: Everything you need to know](https://medium.freecodecamp.com/understanding-flexbox-everything-you-need-to-know-b4013d4dc9af#.44b5tgfom)
* [The Ultimate Flexbox Cheat Sheet](http://www.sketchingwithcss.com/samplechapter/cheatsheet.html)
* [Codrops' Flexbox Reference](https://tympanus.net/codrops/css_reference/flexbox/)
* [Flex-grow 9999 Hack](http://joren.co/flex-grow-9999-hack/)
* [flex-grow is weird. Or is it?](https://css-tricks.com/flex-grow-is-weird/)

Using float is like pre-defining the width of your element. It is not very content focus and is very width focus.

> Flexbox is an efficient way to align and distribute space for dynamic items in a container along an axis.

* Distribute space among flex-items. Expand and shrink items to prevent overflow.
* Flexbox is all about alignment and ordering. It is a smart layout mode that calculates and distributes space.
* Don't always think you need to use media queries. Most of the time a default flexbox can make the site very responsive already.
* Flexbox lets the DOM know that elements on the page have a relationship
* Don't force flexbox to be a grid system, it was not designed for that!
* Flexbox will override floats, table-cell and inline-block. It will not override absolute positioning.

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

`justify-content` defines how flex-items are laid out on the **main axis**. For `row`, the main axis is horizontal, for `column`, it is vertical.

`align-items` defines how flex-items are laid out on the **cross axis**.

`align-content` is very interesting and only happen if flex-items wrap to become multi-line.

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
flex: default;

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

`align-self` align a **single** flex-item along the cross-axis (vertical by default).

## flow-grow

flow-grow will take the remaining space and divide it by the total amount of flex grow values.

If an element has `flex-grow` set to 3 it does not mean that it's 3 times bigger than an element that has `flex-grow` set to 1, but it means that it gets 3 times more pixels added to its initial width than the other element.

## Auto Margin

If you use `margin: auto` alignment on flex-item, the `justify-content` property no longer works.

## Bugs, Advice

* Be careful when you mark `body` as `display: flex`, it will screw up all your block-level elements and make them unable to become 100% full-width since you are essentially marking all immediately children as flex items.

## Video

* [It's Time To Ditch The Grid System](https://www.youtube.com/watch?v=5N9RkIs31Ok)
* [CSS4 Grid: True Layout Finally Arrives](https://www.youtube.com/watch?v=jl164y-Vb5E)