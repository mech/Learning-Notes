# Typography

* [Font Face Observer](https://fontfaceobserver.com/)

By default, use:

* **rem** - for font-size
* **px** - for border-width
* **em** - for everything else like padding, margin, border-radius


```js
document.fonts.ready.then(() => {
  let body = document.body;
  body.classList.toggle('fontzL0ad3d');
});

body {
  font-family: 'Helvetica', 'sans-serif';
}

body {
  font-family: 'T0t411y-R4D-Sans';
}
```

## Web Fonts

* [Web Font Optimization](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/webfont-optimization)
* [A Comprehensive Guide to Font Loading Strategies](https://www.zachleat.com/web/comprehensive-webfonts/)

## Rhythm

* [Implementing baseline rhythm in CSS](https://pilot.co/blog/implementing-baseline-rhythm-in-css/)
* [Vertical and horizontal rhythm](http://us5.campaign-archive2.com/?u=7e093c5cf4&id=564702bd96)
* [Compose to a Vertical Rhythm](https://24ways.org/2006/compose-to-a-vertical-rhythm/)
* [Vertical Rhythm Calculator](https://drewish.com/tools/vertical-rhythm/)

## Typography Scale

* [Type Scale](http://type-scale.com/)
* [Grid Lover](http://www.gridlover.net/try)
* [Truly fluid typography with vh and vw units](https://www.smashingmagazine.com/2016/05/fluid-typography/)

Smaller screen often need smaller font-size, like iPhone display or the small MacBook display. Larger 27" display naturally need bigger font-size. In order for your font to be responsive, you need a system of typography scale.

Instead of defining our typography with an absolute unit like the pixel, we can better design our typography as a scale, as a ratio.

```
// Just use a scalar, times or divides 1.25
2.441em
1.953em
1.563em
1.25em
1em
0.8em
0.64em
0.512em
0.41em
```

## EM

Always tied to font-size. It is good for media queries or grid layout:

```css
/* Given a 1000px width */
/* 15em = 15em * 16px = 240px */
/* 10% = 100px */
/* 1fr = 660px */
grid-template-columns: 15em 1fr 10%;
```

## REM

REM is designed not to be flexible. It is tied to the root (html) element. People sometime just want to be lazy and use the [62.5% hack](https://vasilis.nl/nerd/weird-62-5-antipattern/) to make everything 10px-based. They then use REM unit to prevent the ensuing inheritance mess.

```css
p, li, td, input {
  font-size: 1.6em;
}

li p, li label {
  font-size: 1em; /* Reset it or else will be 1.6em * 1.6em */
}
```

* [The REM fallback with Sass](https://drublic.de/archive/rem-fallback-sass-less/)
* [REMs And Viewport Measurements — Why You Shouldn't Use Them Yet](http://vanseodesign.com/css/rems-and-viewport-measurements/)
* [Why I dislike REM unit](https://vasilis.nl/nerd/dislike-rem-unit/)
* [Use EM and REM for the right use cases](https://vasilis.nl/nerd/use-em-rem-right-use-cases/)
* [rems and ems, and why you probably don’t need them](https://hackernoon.com/rems-and-ems-and-why-you-probably-dont-need-them-664b9ce1e09f)

## Videos

* [Syntax Highlight Everything](https://www.youtube.com/watch?v=s_ooNo2EmMI)