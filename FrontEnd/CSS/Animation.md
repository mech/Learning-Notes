# CSS Animation

* [CSS Versus JavaScript Animations](https://developers.google.com/web/fundamentals/design-and-ux/animations/css-vs-javascript)
* [Meaningful Motion with Action-Driven Animation](http://tobiasahlin.com/blog/meaningful-motion-w-action-driven-animation/)
* [The Illusion of Life](http://www.centolodigiani.com/117722/3078861/work/the-illusion-of-life)
* [Easing](http://easings.net/)
* [Creating Usability with Motion: The UX in Motion Manifesto](https://medium.com/@ux_in_motion/creating-usability-with-motion-the-ux-in-motion-manifesto-a87a4584ddc)
* [How to create fancy revealing animations with these simple CSS tricks](https://hackernoon.com/how-to-create-fancy-revealing-animations-with-these-simple-css-tricks-5b34614ae69a)
* [Anime.js - Greensock may be too heavy](http://animejs.com/)
* [Native-Like Animations for Page Transitions on the Web](https://css-tricks.com/native-like-animations-for-page-transitions-on-the-web/)
* [How you can use simple Trigonometry to create better loaders](https://uxdesign.cc/how-you-can-use-simple-trigonometry-to-create-better-loaders-32a573577eb4)
* [Sculpting Software Animation](https://medium.com/@pasql/sculpting-software-animation-7d818ddcd40a)
* [CSS Animation Tutorials](https://cssanimation.rocks/)

> The reason why I believe motion is so crucial isn't just because it looks nice, but because it changes the way we approach design.
> 
> Rather than thinking in screens, we are now **thinking in stories**. Stories explaining how those screens and the elements in them relate to one another. It's this simple thought, this simple idea really, that already elevates the quality of our interfaces considerably.
> 
> But while motion is all about timing, we rarely consider at which point we should actually start incorporating it into our processes.

## Page Transition

* [How JavaScript works: Under the hood of CSS and JS animations + how to optimize their performance](https://blog.sessionstack.com/how-javascript-works-under-the-hood-of-css-and-js-animations-how-to-optimize-their-performance-db0e79586216)
* [How To Add Page Transitions with CSS and smoothState.js](https://css-tricks.com/add-page-transitions-css-smoothstate-js/)
* [FLIP.js](https://github.com/googlearchive/flipjs)
* [react-router-transition](https://github.com/maisano/react-router-transition)

## UI Thread and Jank

CSS animations have the lowest priority on the UI thread.

Some animations take place on the UI thread. `opacity` and `transform` takes place on the GPU, instead of the CPU, and doesn't rely on the UI thread's availability.

```css
/* Hacks! Try to avoid putting everything on the GPU */
/* Instead, try to include transform over top, left, bottom, right and visibility */
* {
  transform: translateZ(0); /* Don't do this! */
}
```

## Animating `display` properties

`display` is a property that cannot be animated. However for Drawer, sometimes we want to `display: none` the drawer if it is hidden and `display: block` it when transition into view.

* [Animate display block none](https://www.impressivewebs.com/animate-display-block-none/)

## Transform

* Cartesian coordinate - x, y, z
* Spherical coordinate - 360 degree polar system
* Bounding box - any outlines and margins are ignored when calculating bounding box
* Object bounding box - for SVG
* Frame of reference will change according to each successive transform
* Transforms are not cumulative, except for animated transforms, which is additive
* Inline-level boxes can't be transformed (i.e. `<span>`)

Transformed elements have their own stacking context. While the scaled element may be much smaller or larger than it was before the transform, the actual space that the element occupies remains the same.

Order is important for transformation as well as changes to coordinate system (e.g. when element is rotated, its axes change).

```css
/* Transform chain */
transform: rotate(45deg) skewX(-25deg) scaleY(2);
```

* `translate` - `translate3d()`, `translateX()`, `translateY()`, `translateZ()`
* `scale`
* `rotate`
* `skew` - `skewX()`, `skewY()` - there is no 3D skewing
* `matrix` - `matrix3d()`
* `perspective()` - Different from the `perspective` property

```css
/* y will be 0 if omitted */
transform: translate(x, y = 0)

/* All 3 values must be present to consider valid */
transform: translate3d(x, y, z)

/* y will be x if omitted */
transform: scale(x, y = x)
```

### `perspective()` function and `perspective` property

First, we need to enable it using `transform-style: preserve-3d`.

```css
/* Zoom lens */
perspective: 2500px;

/* Fish-eye lens */
perspective: 200px;
```

## Transition

Transforms are without time component. In order to animate, you need transitions and animation.

> Because of this, CSS developers often use CSS animations instead of transitions; animations offer more granularity in creating an arced path, while CSS transitions only allow for moving between two states. However, with some cubic Bézier timing functions, creating an arc with CSS transitions is actually not only possible, but fairly simple.

CSS transitions enable us to smoothly animate CSS properties from an original value to a new value over time as the style re-computation proceeds

* `transition-property`
* `transition-duration` - 100ms to 200ms is best
* `transition-timing-function`
* `transition-delay`
* `transition`

```css
/* All properties at 1s, border-radius at 2s, and opacity at 3s */
transition-property: all, border-radius, opacity;
transition-duration: 1s, 2s, 3s;

/* Shorthand */
transition:
  color 200ms,
  border-width 180ms ease-in 200ms,
  width 2s steps(5, start) 1.4s;
```

### Animatable Properties

* [CSS Transitions Animatable Properties](https://drafts.csswg.org/css-transitions/#animatable-properties)
* [MDN: CSS animated properties](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties)
* `visibility` is sort of animatable even though there is no mid-point between `hidden` and `visible`.

If there is a logical **midpoint** between the initial value and the final value of a property, that property and value type is probably animatable.

Some properties are animatable, but not all values of those properties are animatable. Numeric values tend to be animatable; keywords that can't be converted to numeric values generally aren't.

`top` is a animatable property, but `auto` as one of its value can't be animated.

```css
/* Can't be animated because auto is not a computed value */
height: auto;
```

### Event: `transitionend`

* `propertyName`
* `elapsedTime` - not including transition-delay
* `pseudoElement`

## CSS Animation

Transitions enabled simple animations. You have little control over how the property value interpolation progresses over time. CSS animation changes that using keyframe animations.

With keyframe animations, we can:

* control number of iterations
* iteration behaviors
* what happen before the first animation commences
* pause animation mid-stream

Transitions are implicit while Keyframes are explicit and more granular.

`@keyframes` is how you define reusable animation that will be applied later using `animation-name` property elsewhere.

The entire `@keyframes` specifies the behavior of one full iteration of the animation.

```css
/* You can omit 0% and 100% and UA will use original values */
/* For consistent animation it is recommended you provide 0% and 100% always in order to reset default value */
@keyframes shake {
  0% {
  }
  
  25%, 75% {
  }
  
  to {
  }
}
```

Prohibited animation name as it will break `animation` shorthand property:

```
none, paused, running, infinite, backwards, forwards
```

* `animation-name`
* `animation-duration`
* `animation-iteration-count` - `infinite` | number
* `animation-direction` - `normal` | `reverse` | `alternate` | `alternate-reverse`
* `animation-delay`
* `animation-timing-function`
* `animation-fill-mode` - `none` | `forwards` | `backwards` | `both`
* `animation-play-state` - `running` | `paused`

If `animation-delay: -4s` and `animation-duration: 10s`, the animation will begin immediately but will start approximately 40% of the way through the first animation.

```css
/* Negative delay: The first 3 cycles do not occur */
/* There is also no animationiteration event being fired */
/* The elapsedTime=3 on animationstart event */
.no-iteration {
  animation-name: shake,
  animation-duration: 1s,
  animation-iteration-count: 4;
  animation-delay: -3s;
}
```

```css
/* Shorthand */
/* First time value is always animation-duration, then animation-delay */
/* Snowflake will fall while spinning for 96 seconds */
/* 3s * 32 iteration = 96sec */
/* 1.5s * 64 iteration = 96sec */
/* Spinning will be twice to one falling */
.snowflake {
  animation: 3s ease-in 200ms 32 forwards falling,
             1.5s linear 200ms 64 spinning;
}
```

### Event: `animationstart`, `animationend`, `animationiteration`

When an `animationiteration` event would occur at the same time as an `animationend` event, the `animationiteration` event does not occur.

* `animationName`
* `elapsedTime`
* `pseudoElement`

If there is an `animation-delay`, `animationstart` event will fire once the delay period has expired. Even if there are no iterations, the `animationstart` event still occurs.

If the `animation-iteration-count` is set to `infinite`, the `animationend` event never occurs.

### Animation Chaining

`animation-delay` is frequently used to do animation chaining. But due to lower priority in the UI thread, it can get out of sync very quickly.

Another way of chaining is using JavaScript with `animationend` event.

### Step Timing

The step timing functions aren't Bézier curves, rather, they're **tweening** definitions.

The `steps(count, direction=end)` divides the animation into a series of equal-length steps.

If `animation-duration: 1s`, then `steps(5)` will divide that into five 200ms steps with the element being redrawn to the page 5 times, at 200ms intervals, moving 20% through the animation at each interval. The interval can either be 0%, 20%, 40%, 60% and 80% keyframes or at 20%, 40%, 60%, 80% and 100% keyframes. To choose which side it start, you can give it a `direction` parameter.

## Easing and Bézier

* [cubic-bezier by Lea Verou](http://cubic-bezier.com/#.17,.67,.83,.67)
* [Writing an easing function; a slightly interesting story](https://hackernoon.com/writing-an-easing-function-a-slightly-interesting-story-70ce667c212a)

```
ease        - cubic-bezier(0.25, 0.1, 0.25, 1)
linear      - cubic-bezier(0, 0, 1, 1)
ease-in     - cubic-bezier(0.42, 0, 1, 1)
ease-out    - cubic-bezier(0, 0, 0.58, 1)
ease-in-out - cubic-bezier(0.42, 0, 0.58, 1)
```

## GSAP

* [Writing Smarter Animation Code](https://css-tricks.com/writing-smarter-animation-code/)
* [The Beginner's Guide to the GreenSock Animation Platform](https://medium.freecodecamp.org/the-beginners-guide-to-the-greensock-animation-platform-7dc9fd9eb826)

## Videos

* [Justin McDowell - Bauhaus in the Browser](https://www.youtube.com/watch?v=BaQl84nDBNY)
* [FLIP technique](https://www.youtube.com/watch?v=wQ-jn1KYUkQ)

## People

* [Justin McDowell](http://revoltpuppy.com/)

