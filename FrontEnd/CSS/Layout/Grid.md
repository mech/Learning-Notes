# Grid

* [Grid, Flexbox, Box Alignment: Our New System for Layout](https://24ways.org/2015/grid-flexbox-box-alignment-our-new-system-for-layout/)
* [Liberating layout through CSS Grid](https://cssgrid.cc/)
* [Learn CSS Grid](http://learncssgrid.com/)
* [Does CSS Grid Replace Flexbox?](https://css-tricks.com/css-grid-replace-flexbox/)
* [CSS Grid Layout: How to get Started in 2 Steps — well explained](https://medium.com/flexbox-and-grids/css-grid-layout-how-to-get-started-in-2-steps-well-explained-44fab69d9274)
* [CSS Grid Layout: 3 Vital Differences between Grid Containers & Block Containers](https://medium.com/flexbox-and-grids/css-grid-layout-3-vital-differences-between-grid-containers-block-containers-6f3c39cf3bba)
* [Spring Into CSS Grid](http://jonibologna.com/spring-into-css-grid/)
* [Breaking Out With CSS Grid Layout](https://cloudfour.com/thinks/breaking-out-with-css-grid-layout/)
* [The CSS Fractional Unit (Fr) In Approachable, plain Language](https://medium.com/flexbox-and-grids/the-css-fractional-unit-fr-in-approachable-plain-language-fdc47bd387f7)
* [Stripe Connect: behind the front-end experience](https://stripe.com/blog/connect-front-end-experience)
* [Is it really safe to start using CSS Grid Layout?](https://www.rachelandrew.co.uk/archives/2017/07/04/is-it-really-safe-to-start-using-css-grid-layout/)
* [How to Efficiently Master the CSS Grid in a Jiffy](https://medium.com/flexbox-and-grids/how-to-efficiently-master-the-css-grid-in-a-jiffy-585d0c213577)
* [The Difference Between Explicit and Implicit Grids](https://css-tricks.com/difference-explicit-implicit-grids/)

With 18 new CSS Grid properties, there are many ways to achieve the same thing with the Grid layout. This is what makes it overwhelming.

> When is comes to creating consistent space between items, Grid beats any other layout method hands down.

Remember, the CSS Grid does not **physically** exist. It is all invisibles lines.

## Differences with Flexbox

* Flexbox is one-dimensional, it can be horizontally or vertically, but never both at the same time
* CSS Grid is a two-dimensional system for placing elements
* Use flexbox for the alignment options it brings on a single line/dimension.

Layouts that previously were difficult, sometimes even impossible to create, are now within easy reach. New functions such as the MinMax in combination with new sizing units such as the `fr` offer all types of responsive layout possibilities.

Grid is different from all the layout techniques we've used in the past because it is the only solution that works from the container in (credit to Rachel Andrew for this concept). It calls for a big picture view of the grid you have in mind, as opposed to sizing each item individually, which may sometimes lead to a "missing the forest for the trees" situation.

## Fallback

* Use Feature Queries
* [Grid "fallbacks" and overrides](https://rachelandrew.co.uk/css/cheatsheets/grid-fallbacks)
* [Basic grid layout with fallbacks using feature queries](https://www.chenhuijing.com/blog/basic-grid-with-fallbacks/)

```css
/* For browser like IE11 which support Flexbox, it is still fine */
main {
  display: flex;
}

/* For those more modern browsers, it is CSS Grid for them all */
@supports (display: grid) {
  main {
    display: grid;
  }
}
```

Use a Feature Query when you want to apply a mix of old and new CSS, but only when the new CSS is supported.

For browsers that don't have `@supports` like IE9-10-11, all the styles within the `@supports` block is totally ignored.

## Grid Container

Grid does not require a whole slew of containers and classes just for layout purposes. In fact, it is the first time in the history of the web that presentation and content are truly separated.

Establishes a **grid-formatting context** in contrast to block-formatting context.

```css
/* Using fractional units */
display: grid;
grid-template-columns: 1fr 2fr 1fr; /* (1 + 2 + 1) ÷ width */
grid-template-columns: 25% 50% 25%; /* Same */
```

```css
/* A mixture of fixed and flexible columns */

/* Given a 1000px width */
/* 15em = 15em * 16px = 240px */
/* 10% = 100px */
/* 1fr = 660px */
grid-template-columns: 15em 1fr 10%;
```

## Grid Items

Bulk of the work can be done at the Grid Container. Items will just do their automatic layout thing (flow into the cells of grid automatically). But you can have tight control over the placement of each Grid Item also.

```css
.item {
  grid-row-start: 1;
  grid-column-start: 1;
}

/* Given a 3 columns grid, it has line 1 to 4 */
/* This will stay in 2nd cell and span 2 columns */
.item-that-span-multiple-track {
  grid-column-start: 2;
  grid-column-end: 4;
}

.item-same-as-above {
  grid-column: 2 / span 2;
}
```

## Gutter

```css
.grid {
  display: grid;

  grid-gap: 10px;
  grid-row-gap: 5px;
  grid-column-gap: 5px;
}
```

Being able to define an explicit gutter between the elements is one of the big advantages over flexbox or float-based layout methods.

Just two simple lines of CSS on the grid **parent** (container) are needed to create a consistent space between the grid items.

A very different approach compared to the older methods where you had to specify a space (margin) on the **element**. Which would come with some problems such as unwanted space at the edges of the of the grid. This space then had to be removed on that specific element...but when the elements wrap at smaller screens a different element would sit at the end...creating a 'chasing space' type of nightmare.

## Grid Lines and Tracks

* [Deep Dive into Grid Layout Placement](https://blogs.igalia.com/mrego/2016/02/01/deep-dive-into-grid-layout-placement/)

Grid Lines start from the outermost edges. If you have 3 columns, then you have 4 lines. If you have 5 rows, then you have 6 lines.

A Grid Track is either a column or a row from the start to the end.

```css
/* To create a 2 grid tracks */
grid-template-rows: repeat(2, minmax(80px, auto));
```

## Subgrids

## Fractional Unit

* [What You Didn't know about the CSS Fractional Unit](https://medium.com/flexbox-and-grids/what-you-didnt-know-about-the-css-fractional-unit-580bd62647e8)

## minmax() Function

```css
/* The first row has a min height of 80px but can grow if required by its content */
grid-template-rows: minmax(80px, auto);
```

```css
/* The 3rd column should never be less than 5em wide */
grid-template-columns: 15em 4.5fr minmax(5em, 3fr) 10%;
```

## People

* [Manuel Rego Casasnovas](https://blogs.igalia.com/mrego/)

## Videos

* [Introduction To CSS Grids](https://www.youtube.com/watch?v=H3LRtAm2SOo)
* [CSS Grid Layout - Rachel Andrew | February 2017](https://www.youtube.com/watch?v=N5Lt1SLqBmQ)
* [CSS4 Grid: True Layout Finally Arrives (Jen Kramer) - Full Stack Fest 2016](https://www.youtube.com/watch?v=axVw1Zduqn0)
* [Start Using CSS Grid Layouts Today](https://youtu.be/tjHOLtouElA?list=PLBzScQzZ83I_n5kvxmUaRNZvc_vsCuEQD)