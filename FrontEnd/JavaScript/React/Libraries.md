# Libraries

https://github.com/hsnaydd/moveTo/

https://dollarshaveclub.github.io/stickybits/

* [**Awesome React Components & Libraries**](https://github.com/brillout/awesome-react-components/blob/master/readme.md)
* [React Desktop](http://reactdesktop.js.org/)
* [Smart modules for React](https://github.com/smalldots/smalldots)
* [Best Practices on building a UI component library for your company](https://www.youtube.com/watch?v=j8eBXGPl_5E)
* [Carte Blanche - Like Storybook?](https://github.com/carteb/carte-blanche)
* [CUID compared to UUID or shortid](https://github.com/ericelliott/cuid)

## Visual

* [React Color](https://casesandberg.github.io/react-color/)

## UI Libraries

* [iOS HIG](https://developer.apple.com/ios/human-interface-guidelines/resources/)
* [instructure-ui](https://instructure.github.io/instructure-ui/)
* [Semantic UI React](https://react.semantic-ui.com/introduction)
* [React Toolbox](http://react-toolbox.com/#/)
* [Ant Design of React](https://ant.design/docs/react/introduce)
* [Wix Style - React](https://github.com/wix/wix-style-react)
* [MuleSoft](http://ux.mulesoft.com/#/playground/Row)
* [react-primitives](https://github.com/lelandrichardson/react-primitives)
* [Blueprint](http://blueprintjs.com/)

## Case Study

* [react-soundplayer](http://labs.voronianski.com/react-soundplayer/)
* [react-aria](https://github.com/souporserious/react-aria)

## PDF

* [Rendering PDFs with React Components](https://themeteorchef.com/tutorials/rendering-pdfs-with-react-components)
* [react-pdf](https://github.com/nnarhinen/react-pdf)

## Show/Hide

* [render-if](https://github.com/ajwhite/render-if)
* [react-only-if](https://github.com/MicheleBertoli/react-only-if)
* [react-hoverbox](https://github.com/wix/react-hoverbox)

## Table (Filtering, Pagination)

* [reactable](https://github.com/glittershark/reactable)
* [react-table](https://github.com/tannerlinsley/react-table)

## Modal and Dialog

* [react-portal](https://github.com/tajo/react-portal)
* [react-slot-fill](https://github.com/camwest/react-slot-fill)
* [react-waypoint](https://github.com/brigade/react-waypoint)

## Auto-complete and Instant Search

* [RDropdown](https://github.com/jamhall/rdropdown)
* [GooglePlaceAutocomplete](https://github.com/ydeshayes/googlePlaceAutocomplete)
* [Algolia](https://community.algolia.com/react-instantsearch/)

## Date Picker and Calendar

* [react-big-calendar](https://github.com/intljusticemission/react-big-calendar)
* [react-calendar-timeline](https://github.com/namespace-ee/react-calendar-timeline)
* [react-dates from Airbnb](https://github.com/airbnb/react-dates)
* [react-day-picker](http://react-day-picker.js.org)

---

* [The Past, Present, and Future of JavaScript Date and Time APIs](https://www.youtube.com/watch?v=aVuor-VAWTI)
* [js-joda](https://github.com/js-joda/js-joda)

Moment.js is mutable and may become immutable in the future so there is no need to clone anymore.

```js
const format = require('date-fns/format')
const addDays = require('date-fns/addDays')

const d = new Date(2017, 1, 1)
const s = format(d, 'DD/MM/YYYY')

const a = addDays(d, 10)
```

## File Upload

* [Drag and drop file upload](https://codepen.io/pixelass/pen/dpyBOd?editors=0010)

```html
<input type="file" accept="*">
```

```js
input.addEventListener('change', () => {
  const file = input.files[0]
  
  const metadata = {
    name: file.name,
    type: file.type,
    size: file.size
  }
})
```

## Sortable and Drag and Drop

* [Some react-dnd example](https://gist.github.com/krzysu/1b391ae0e3c87d0c654cdf6d5a409632)

## D3

* [A starting point on using D3 with React](https://blog.sicara.com/a-starting-point-on-using-d3-with-react-869fdf3dfaf#.aood1myab)

## Images

* [css-aspect-ratio](https://github.com/sgomes/css-aspect-ratio)
* [Low Quality Image Placeholders (LQIP) for Webpack](https://github.com/zouhir/lqip-loader)

## Editor

* [Dante 2](https://michelson.github.io/dante2/)
* [Slate](https://github.com/ianstormtaylor/slate)
* [react-in-markdown](https://github.com/kitze/react-in-markdown)
* [markdown-it](https://github.com/markdown-it/markdown-it)
* [react-mde](https://github.com/andrerpena/react-mde)
* [Anchorme - Tiny, fast, efficient, feature rich Javascript library to detect links/URLs/Emails in text and convert them to clickable HTML anchor links](https://alexcorvi.github.io/anchorme.js/)