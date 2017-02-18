# Float

Float is a hack, right after table-based layout! It features rows and cells. We put the floats on the cells and clear the row.

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

### Margin Collapsing

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

Margin collapsing can be interrupted by factors such as paddings and borders on parent elements.

### Inline Element

* Inline non-replaced element - span, em (`width` and `height` a non-factor here)
* Inline replaced element - images, forms

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