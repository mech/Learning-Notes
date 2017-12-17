# BEM

* [CSS Utility Classes and "Separation of Concerns"](https://adamwathan.me/css-utility-classes-and-separation-of-concerns/)
* [Specificity Visualizer](https://francescoschwarz.de/en/blog/introducing-the-specificity-visualizer/)

A lot of semantic CSS class names have a lot in common from a design perspective.

> We don't want to use content-specific names because then our component could only be used in one context

```html
<div class="card rounded shadow">
</div>
```

Well maybe it's housed in a card. Not all cards have a shadow though so we could have a `.card--shadowed` modifier, or we could create a `.shadow` utility that could be applied to any element. That sounds more reusable, so let's do that.

It turns out some of the cards on our site don't have rounded corners, but this one does. We could make it `.card--rounded`, but we have other elements on the site that are sometimes rounded the same amount too, and those aren't cards. A `.rounded` utility would be more reusable.

```css
.text-center {
  text-align: center;
}

.px-4 {
  padding-right: 1rem;
  padding-left: 1rem;
}

.pb-16 {
  padding-bottom: 4rem;
}

.mx-auto {
  margin-left: auto;
  margin-right: auto;
}

.constrain-sm {
  max-width: 30rem;
  flex-basis: 30rem;
}
```