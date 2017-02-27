# React Animation

* [React Page Transition Animations](https://medium.com/front-end-hacking/react-page-transition-animations-9d18c90a9831#.jpe9r2a9b)

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