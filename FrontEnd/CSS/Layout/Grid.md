# Grid

* [Learn CSS Grid](http://learncssgrid.com/)
* [Does CSS Grid Replace Flexbox?](https://css-tricks.com/css-grid-replace-flexbox/)
* [CSS Grid Layout: How to get Started in 2 Steps — well explained](https://medium.com/flexbox-and-grids/css-grid-layout-how-to-get-started-in-2-steps-well-explained-44fab69d9274)
* [CSS Grid Layout: 3 Vital Differences between Grid Containers & Block Containers](https://medium.com/flexbox-and-grids/css-grid-layout-3-vital-differences-between-grid-containers-block-containers-6f3c39cf3bba)
* [Spring Into CSS Grid](http://jonibologna.com/spring-into-css-grid/)
* [Breaking Out With CSS Grid Layout](https://cloudfour.com/thinks/breaking-out-with-css-grid-layout/)
* [The CSS Fractional Unit (Fr) In Approachable, plain Language](https://medium.com/flexbox-and-grids/the-css-fractional-unit-fr-in-approachable-plain-language-fdc47bd387f7)
* [Stripe Connect: behind the front-end experience](https://stripe.com/blog/connect-front-end-experience)

## Grid Container

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

## Subgrids

## minmax() Function

```css
/* The 3rd column should never be less than 5em wide */
grid-template-columns: 15em 4.5fr minmax(5em, 3fr) 10%;
```

## Videos

* [Introduction To CSS Grids](https://www.youtube.com/watch?v=H3LRtAm2SOo)
* [CSS Grid Layout - Rachel Andrew | February 2017](https://www.youtube.com/watch?v=N5Lt1SLqBmQ)
* [CSS4 Grid: True Layout Finally Arrives (Jen Kramer) - Full Stack Fest 2016](https://www.youtube.com/watch?v=axVw1Zduqn0)
* [Start Using CSS Grid Layouts Today](https://youtu.be/tjHOLtouElA?list=PLBzScQzZ83I_n5kvxmUaRNZvc_vsCuEQD)