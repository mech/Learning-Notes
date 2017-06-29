# React Animation

* [React Page Transition Animations](https://medium.com/front-end-hacking/react-page-transition-animations-9d18c90a9831#.jpe9r2a9b)
* [Moving Beyond Animations to User Interactions at 60 FPS in React Native](https://medium.com/@talkol/moving-beyond-animations-to-user-interactions-at-60-fps-in-react-native-b6b1fa0ba525#.v3vy9yw0i)
* [material-motion-js](https://github.com/material-motion/material-motion-js)
* [Getting Reactive with CSS](http://slides.com/davidkhourshid/getting-reactive-with-css#/)
* [Getting Reactive with CSS - Video](https://www.youtube.com/watch?v=4IRPxCMAIfA)
* [The principles of React Router are such that you can wrap up complex animation code into declarative components - Ryan Florence](https://github.com/tkh44/data-driven-motion/blob/master/demo/src/App.js#L187-L191)

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

## Libraries

* [React Overdrive - Simple and powerful animations](https://react-overdrive.now.sh/)
* [react-move](https://github.com/tannerlinsley/react-move)
* [mo.js](http://mojs.io/)
* Web Animations API - not mature yet

## Physicality, Velocity, Spring, Realism, Snapping, Friction
