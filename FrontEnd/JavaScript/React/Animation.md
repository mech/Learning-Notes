# React Animation

* [**React Animations in Depth**](https://medium.com/react-native-training/react-animations-in-depth-433e2b3f0e8e)
* [How to build animated microinteraction in React](https://medium.freecodecamp.org/how-to-build-animated-microinteractions-in-react-aab1cb9fe7c8)
* [Airbnb - Behind the scenes of our new open-source animation tool](https://airbnb.design/introducing-lottie/)
* [React Page Transition Animations](https://medium.com/front-end-hacking/react-page-transition-animations-9d18c90a9831#.jpe9r2a9b)
* [Moving Beyond Animations to User Interactions at 60 FPS in React Native](https://medium.com/@talkol/moving-beyond-animations-to-user-interactions-at-60-fps-in-react-native-b6b1fa0ba525#.v3vy9yw0i)
* [material-motion-js](https://github.com/material-motion/material-motion-js)
* [Getting Reactive with CSS](http://slides.com/davidkhourshid/getting-reactive-with-css#/)
* [Getting Reactive with CSS - Video](https://www.youtube.com/watch?v=4IRPxCMAIfA)
* [The principles of React Router are such that you can wrap up complex animation code into declarative components - Ryan Florence](https://github.com/tkh44/data-driven-motion/blob/master/demo/src/App.js#L187-L191)
* [React at 60fps](https://hackernoon.com/react-at-60fps-4e36b8189a4c)
* [One weird trick to performant touch-response animations with React](https://medium.com/@owencm/one-weird-trick-to-performant-touch-response-animations-with-react-9fe4a0838116)
* [Val Head - Getting started with animation in React](http://us2.campaign-archive1.com/?u=6fbaddc8c1fce7588d1a35cb2&id=61966a3f9a)
* [react-stack-grid - Look at the animation example](https://github.com/tsuyoshiwada/react-stack-grid)
* [Build a Reusable Scroll List Component with Animated scrollTo in React](https://codeburst.io/build-a-reusable-scroll-list-component-with-animated-scrollto-in-react-4b4da8815f5b)
* [Animated page transitions with React Router 4, ReactTransitionGroup and Animated](https://hackernoon.com/animated-page-transitions-with-react-router-4-reacttransitiongroup-and-animated-1ca17bd97a1a)
* [Demystifying requestAnimationFrame](https://medium.com/@bkakadiya42/demystifying-the-requestanimationframe-867c3db6c217)
* [Animating React Components with CSS and Styled-Components](https://codeburst.io/animating-react-components-with-css-and-styled-components-cc5a0585f105)
* [Animating React Applications](https://x-team.com/blog/animating-react-applications/)

React ships with react-addons-css-transition-group which is a component that helps us build animations in a declarative way.

We wrap the component to which we want to apply the animation with it:

```js
// Apply fade-appear as soon as it gets rendered
// On the next tick, apply fade-appear-active to fire the animation
// You can also use *-enter and *-enter-active classes when new
// element is added as a child of the transition group
const Transition = () => (
  <CSSTransitionGroup
    transitionName="fade"
    transitionAppear
    transitionAppearTimeout={500}
  >
    <h1>Hello</h1>
  </CSSTransitionGroup>
)
```

```css
.fade-appear {
  opacity: 0.01;
}

.fade-appear.fade-appear-active {
  opacity: 1;
  transition: opacity .5s ease-in;
}
```

The `*-enter` and `*-enter-active` classes are applied when a new element is added as a child of the transition group.

## GSAP - Greensock

* [React meets GSAP](https://medium.com/@marcmintel/react-meets-gsap-c6dd82edeb72)

## Libraries

* [React Overdrive - Simple and powerful animations](https://react-overdrive.now.sh/)
* [react-move](https://github.com/tannerlinsley/react-move)
* [mo.js](http://mojs.io/)
* Web Animations API - not mature yet
* [Flight - Ultra Simple Animation Compositions for React](http://www.react-flight.io/)
* [react-layout-transition](https://github.com/bkazi/react-layout-transition)

## Physicality, Velocity, Spring, Realism, Snapping, Friction

## Videos

* [Animating the Virtual DOM - Sarah Drasner](https://www.youtube.com/watch?v=W5AdUcJDHo0)

## People

* [Jason Brown - Animated](http://browniefed.com/)