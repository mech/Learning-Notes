# Component Style

* [All the CSS-in-JS options you have](https://github.com/MicheleBertoli/css-in-js)
* [Don’t pass CSS classes between components](https://brigade.engineering/don-t-pass-css-classes-between-components-e9f7ab192785#.f82zjt3f4)
* [CSS in JS: The Argument Refined - The Este approach](https://medium.com/@steida/css-in-js-the-argument-refined-471c7eb83955#.j96f9jrws)
* [Fela](http://fela.js.org/)
* [JSS - The one chosen by Material-UI](http://cssinjs.org/?v=v6.5.0)

```js
<Button className="button-icon-check">Okay</Button>

<Button icon="check">Okay</Button>
```

## Storybook

* [Algolia](https://community.algolia.com/instantsearch.js/react/storybook)

## Requirements

* Document vs App mindset
* Easy to debug at Dev Tool, don't rely on element.style
* Write styles to an actual stylesheet - this ruled out styled-components which is runtime
* Fast to first paint
* Server-render
* Works with pseudo classes and media queries directly
* Aware of theming

## Variables

* Keylines
* Spacing
* Margins
* Fonts

## Benefits of CSS in JS

Do you have BEM like this all over your code base:

```html
<button class="btn btn--primary">Submit</button>
```

If you need to change style, you need to go through all HTML files that are using the BEM component.

* Global CSS do no good for component-based styling
* Your `button` style should be isolated and does not care the rest of your pages look like. The styling of the button component shouldn't be used anywhere else.

## CSS Modules

* [react-css-modules](https://github.com/gajus/react-css-modules)

```js
loader: 'style!css?modules&localIdentName=[local]--[hash:base64:5]'
```

**Atomic CSS Modules** - Using Functional CSS together with CSS Modules.

```css
.mb0 {
  margin-bottom: 0;
}

.fw6 {
  font-weight: 600;
}

.title {
  composes: mb0 fw6;
}
```

```js
<h2 className={styles.title}>Hello React</h2>

// Result in
<h2 class="title--3JCJR mb0--21SyP fw6--1JRhZ">Hello React</h2>
```

## styled-components

* [Tagged Template Literal](http://exploringjs.com/es6/ch_template-literals.html)
* [Comparison with other solutions](https://github.com/styled-components/comparison)
* [Glen Maddern - Styling React Apps with Styled Components](https://www.youtube.com/watch?v=qu4U7lwZTRI)
* [Glenn Maddern - The Future of Reusable CSS](https://www.youtube.com/watch?v=XR6eM_5pAb0)
* [Styled-Component - Production Patterns](https://medium.com/@jamiedixon/styled-components-production-patterns-c22e24b1d896#.f0rayh3o3)
* [The magic behind styled-components](https://mxstbr.blog/2016/11/styled-components-magic-explained/)

> @simurai Between em and currentColor, who needs variables? - [Styling with Strings]
(https://www.youtube.com/watch?v=jPOBVaomzLE)

Benefits:

* Switch styles based on incoming props rather than appending new class names to HTML - (i.e. `isOpen` props)
* Clearer JSX with little `<div>` littering around
* Composing styles