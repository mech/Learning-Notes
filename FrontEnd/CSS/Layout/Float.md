# Float

Float is a hack, right after table-based layout! It features rows and cells. We put the floats on the cells and clear the row.

For a long time, floated elements where the basis of all web layout schemes. This is largely because of the property `clear`. But floats were never meant for layout; their use as a layout tool was a hack.

A floated element is, in some ways, removed from the normal flow of the document, although it still have influence over the rest of the document.

Margins around floated elements do not collapse.

Floated element generates a block box, regardless of the kind of element it is. Thus, if you float a link, even though the element is inline and would ordinarily generate an inline box, it generates a block box when floated.

Floated element will expand to contain any floated descendants. Thus, you could contain a float within its parent by floating the parent also.

```css
.col-1 {
  float: left;
  margin-left: 4%;
  width: 20%;
}

.row::after {
  content: "";
  display: table;
  clear: both;
}
```

**Flexbox example**

```css
$columns: 12;
$gutter: 12px;
$padding: 10px;

.column {
  flex-basis: calc(100% / #{$columns});
  margin: 0 $gutter;
  padding: 0 $padding;
  
  @for $i from 2 through 12 {
    &._#{$i} {
      flex-basis: calc(100% / #{$columns * $i});
    }
  }
}

.grid, .row {
  display: flex;
  flex-wrap: wrap;
}

.row {
  margin: 0 ($padding + $gutter) * -2;
}
```

```html
<div class="grid">
  <div class="column _4"></div>
  <div class="column _4"></div>
  <div class="column _2"></div>
  <div class="column _2"></div>
</div>
```

## Box Model

CSS is all about rectangular boxes (element box). At the center is the content area surrounded by paddings, borders, outlines and margins.

Padding cannot be negative, but margins can. Padding can't be `auto`, but margin can. Border cannot accept percentage values.

```css
padding: auto; /* Don't make sense*/

/* Make sense */
margin: auto;
width: auto;
```

There are many element boxes:

* Block box - generate new lines before and after the box
* Inline box
* Inline-block box - Since CSS2.1
* List-item box
* Run-in box - Another interesting block/inline hybrid

Any element that accept `width` and `height` can apply `box-sizing` property.

If you set `margin-left: auto` and `margin-right: auto` and `width: auto`, the both margins will become zero and the `width` will be as wide as the containing block.

```css
width: auto;        /* Essentially become 100% */ 
margin-left: auto;  /* Become zero */
margin-right: auto; /* Become zero */
```

Unlike their left-and-right counterpart, if you set `margin-top` and `margin-bottom` to `auto`, they will both be evaluated to 0. This is why vertical centering is impossible for normal flow.

### box-sizing

By default, padding is added to the **content area**, and the content area's size is determined by `width` and `height`.

### Margin Collapsing

* [What's the Deal with Collapsible Margins?](https://bitsofco.de/collapsible-margins/)
* [Single-direction margin declarations](https://csswizardry.com/2012/06/single-direction-margin-declarations/)

One important aspect of vertical formatting is the collapsing of vertically adjacent margins. Collapsing applies only to margins. Padding and borders, where they exist, never collapse with anything.

`margin-bottom` of previous element combined with `margin-top` of next element into a single margin of the largest margin.

Margins of floating and absolutely positioned elements NEVER collapsed.

> There is only margin-top OR only margin-bottom. Choose one and stick to it!

By only ever using `margin-bottom`, every element is in charge of how much space there should be below it. But some people like to use padding instead for paragraph:

```css
p {
  margin: 0;
  padding: 0.5em 10px;
}
```

Margin collapsing can be interrupted by factors such as paddings and borders on parent elements. If you give it a border, it will not collapse! This happen because the margin of the parent is no longer in direct contact with the margin of the child.

### Inline Element

* Inline non-replaced element - span, em (`width` and `height` a non-factor here)
* Inline replaced element - images, forms (in theory CSS does not style the contents of replaced elements like checkboxes)

Know that all inline elements have a `line-height`, whether it's explicitly declared or not. This value greatly influences the way inline elements are display.

Declaring `line-height` on a block-level element sets a **minimum** line box height for the **content** of that block-level element.

`line-height` is set in relation to the `font-size` of the element itself, not the parent element.

Padding, margins and borders may be applied to inline non-replaced elements, but they do not influence the height of the line box at all. However, they can affect left and right side of the element.

> Block-level elements are in many ways easy to understand, and affecting their layout is typically a simple task. Inline elements, on the other hand, can be trickier to manage, as a number of factors come into play, not least of which is whether the element is replaced or non-replaced.

## Paddings, Borders, Outlines, and Margins

You almost do not want to be percentage in `padding` as it is relative to the `width` of the parent element. You can however use `em` for a much more constant behavior.

```css
padding: 5%; /* will have drastic effect when width changes */

padding: 0.5em;
```

A border with no style do not exist, even if it has a massive `border-width`.

## Positioning

Positioning allows you to define exactly where element boxes will appear relative to where they would ordinarily be.

```
position: static | relative | sticky | absolute | fixed | inherit
```

Absolutely positioned elements will always be block-level, regardless of the type of box it would have generated if it were in normal flow.

When it comes to positioning, the **containing block** depends entirely on the type of positioning.

Positioned elements can be positioned outside of their containing block. This is very similar to the way in which floated elements can use negative margins to float outside of their parent's content area.

It also suggests that the term "containing block" should really be "positioning context" but since the specification uses containing block, so will I.

```
offset properties: top, right, bottom, left
```

Positive values cause inward offsets, moving the edges toward the center of the containing block, and negative values cause outward offsets.

If you put `bottom: 0` on an absolutely positioned block, setting a `height: 100%` add nothing to the layout:

```css
position: absolute;
top: 0;
bottom: 0;
height: 100%; /* Do nothing actually */
```

### Stacking Context

