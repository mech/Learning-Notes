# Libraries

https://github.com/hsnaydd/moveTo/

https://dollarshaveclub.github.io/stickybits/

* [**Awesome React Components & Libraries**](https://github.com/brillout/awesome-react-components/blob/master/readme.md)
* [React Desktop](http://reactdesktop.js.org/)
* [Smart modules for React](https://github.com/smalldots/smalldots)
* [Best Practices on building a UI component library for your company](https://www.youtube.com/watch?v=j8eBXGPl_5E)
* [Carte Blanche - Like Storybook?](https://github.com/carteb/carte-blanche)
* [CUID compared to UUID or shortid](https://github.com/ericelliott/cuid)

## For Development

* [react-inspector](https://github.com/xyc/react-inspector)

## Visual

* [React Color](https://casesandberg.github.io/react-color/)
* [Pure CSS Tooltips](https://medium.freecodecamp.org/a-step-by-step-guide-to-making-pure-css-tooltips-3d5a3e237346)

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
* [buffer-components](https://github.com/bufferapp/buffer-components)

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

> Tables are effective because the nature of enterprise applications requires users to view rows of data simultaneously, scanning through alerts, comparing data and looking at data in any specific order of the user's choice.
> 
> What you are seeing below might seem like a very regular table pattern and might seem like there is nothing wrong about the usability of it at first, but as you get deeper into working on it, one would start realizing the quirks of operating it.

When paging, you can use arrow key. We also need to buffer and throttle requests

If there are only 2 or 3 pages worth of data, why not just show all?

* [sematable](https://github.com/sematext/sematable)
* [Facebook's fixed-data-table](https://github.com/facebook/fixed-data-table)
* [reactable](https://github.com/glittershark/reactable)
* [react-table](https://github.com/tannerlinsley/react-table)
* [csvtotable](https://github.com/vividvilla/csvtotable)
* [react-sticky](https://github.com/captivationsoftware/react-sticky)
* [Design better tables for enterprise applications](https://uxdesign.cc/designing-better-tables-for-enterprise-applications-f9ef545e9fbd)
* [Mailchimp Tables Pattern - See Slats also](https://ux.mailchimp.com/patterns/tables)
* [Design better data tables](https://uxdesign.cc/design-better-data-tables-4ecc99d23356)
* [Design Better Data Tables](https://medium.com/mission-log/design-better-data-tables-430a30a00d8c)
* User tabular figures - `font-feature-settings: "tnum" 1`
* [Free Work Sans has excellent true tabular lining figures](https://fonts.google.com/specimen/Work+Sans)

## Spreadsheet

* [Handsontable](https://handsontable.com/)

## Modal and Dialog

* [react-portal](https://github.com/tajo/react-portal)
* [react-slot-fill](https://github.com/camwest/react-slot-fill)
* [react-waypoint](https://github.com/brigade/react-waypoint)

## Auto-complete and Instant Search

* [RDropdown](https://github.com/jamhall/rdropdown)
* [GooglePlaceAutocomplete](https://github.com/ydeshayes/googlePlaceAutocomplete)
* [Algolia](https://community.algolia.com/react-instantsearch/)
* [react-categorized-tag-input](http://erizocosmi.co/react-categorized-tag-input/)

## Date Picker and Calendar

* [Making input type=date complicated](https://medium.com/samsung-internet-dev/making-input-type-date-complicated-a544fd27c45a)
* [Designing The Perfect Date And Time Picker](https://www.smashingmagazine.com/2017/07/designing-perfect-date-time-picker/)
* [react-big-calendar](https://github.com/intljusticemission/react-big-calendar)
* [react-calendar-timeline](https://github.com/namespace-ee/react-calendar-timeline)
* [react-dates from Airbnb](https://github.com/airbnb/react-dates)
* [react-day-picker](http://react-day-picker.js.org)
* [calreact](https://github.com/learnetto/calreact)
* [spectre](https://picturepan2.github.io/spectre/experimentals.html#calendars)

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

## Tabs

* [react-tabs-redux](https://github.com/patrik-piskay/react-tabs-redux)

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
* [react-mde - React Markdown Editor](https://github.com/andrerpena/react-mde)
* [Anchorme - Tiny, fast, efficient, feature rich Javascript library to detect links/URLs/Emails in text and convert them to clickable HTML anchor links](https://alexcorvi.github.io/anchorme.js/)
* [Alloy Editor](http://alloyeditor.com/)
* [Creating a rich text editor - Part 1 - Barebones Editor](http://bitwiser.in/2017/04/11/creating-rte-barebones-editor.html)