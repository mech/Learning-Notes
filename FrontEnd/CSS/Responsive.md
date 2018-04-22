# Responsive

```css
.container {
  width: 90%;
  max-width: 1024px;
  margin: 0 auto;
}

/* Mobile-first with min-width */
/* By default, it is stacked vertically with no float */
@media screen and (min-width: 700px) {
  .sidebar {
    width: 24.4140625%; /* 250/1024 = 0.244140625 */
    float: left;
  }
}
```

## CSS Variables

* [Learn CSS variables](https://scrimba.com/g/gcssvariables)
* [How to make responsiveness super simple with CSS Variables](https://medium.freecodecamp.org/how-to-make-responsiveness-super-simple-with-css-variables-8c90ebf80d7f)

## `calc()`

`calc()` is very useful for responsive design when you want to take value away from a percentage value.

## Viewport Units

* [CSS Locks](https://fvsch.com/code/css-locks/)
* [Unexpected power of viewport units in CSS](https://www.lullabot.com/articles/unexpected-power-of-viewport-units-in-css)
* [Viewport unit based typography](https://zellwk.com/blog/viewport-based-typography/)
* [Viewport height is taller than the visible part of the document in some mobile browsers](https://nicolas-hoizey.com/2015/02/viewport-height-is-taller-than-the-visible-part-of-the-document-in-some-mobile-browsers.html)
* [Vertical limit](https://adactio.com/journal/11690)
* [URL Bar Resizing](https://developers.google.com/web/updates/2016/12/url-bar-resizing)

```css
h1 {
  font-size: calc(100% + 5vw);
}
```

## Media Queries

* [PX, EM or REM Media Queries?](https://zellwk.com/blog/media-query-units/)
* [On container queries](https://ethanmarcotte.com/wrote/on-container-queries/)

We have no idea what screen size our users have. We just can't control that. But there's a few things we do know. We know our brand and our UI. And we know our content. Content isn't just paragraphs of text. It's the things that are held or included in something.

We should always start with content. Without content, design is meaningless. We design to help users consume content. We don't use content to help users enjoy our designs.

> We often start designing with a box. And then we put smaller boxes inside it. Then later will fill in these boxes with actual content. As Frank Chimero beautifully explains in The Web's Grain, this is just about the worst thing we can do.

```js
// See https://medium.com/airbnb-engineering/rearchitecting-airbnbs-frontend-5e213efc24d2
// for ShowAt and HideAt
import HideAt from '../HideAt'
import ShowAt from '../ShowAt'

render() {
  return (
    <div key={roomTypeId}>
      <ShowAt breakpoint="mediumAndAbove">
      </ShowAt>
      
      <HideAt breakpoint="mediumAndAbove">
      </HideAt>
    </div>
  )
}
```

## Images

`object-fit: cover`

