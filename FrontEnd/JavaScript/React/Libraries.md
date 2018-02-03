# Libraries

**https://inclusive-components.design/**

> Look at **jQuery UI** or **YUI** for props and widgets inspiration? - [Compound Components](https://www.youtube.com/watch?v=hEGg-3pIHlE)

https://github.com/hsnaydd/moveTo/

https://dollarshaveclub.github.io/stickybits/

* [200+ components](https://www.javascriptstuff.com/react-components/)
* [**JS.Coach**](https://js.coach/)
* [**Awesome React Components & Libraries**](https://github.com/brillout/awesome-react-components/blob/master/readme.md)
* [React Desktop](http://reactdesktop.js.org/)
* [Smart modules for React](https://github.com/smalldots/smalldots)
* [Best Practices on building a UI component library for your company](https://www.youtube.com/watch?v=j8eBXGPl_5E)
* [Carte Blanche - Like Storybook?](https://github.com/carteb/carte-blanche)
* [CUID compared to UUID or shortid](https://github.com/ericelliott/cuid)
* [reflective-bind](https://github.com/flexport/reflective-bind)

https://github.com/jaredpalmer/react-fns

## Ajax

* [better-fetch](https://github.com/Swizec/better-fetch)
* [react-idle](https://reacttraining.com/react-idle/)

## For Development

* [react-inspector](https://github.com/xyc/react-inspector)

## Toggle

* [react-toggled](https://github.com/kentcdodds/react-toggled)

## Visual

* [React Color](https://casesandberg.github.io/react-color/)
* [Pure CSS Tooltips](https://medium.freecodecamp.org/a-step-by-step-guide-to-making-pure-css-tooltips-3d5a3e237346)
* [Popper.js](https://popper.js.org/)
* [Pace.js - For loading](http://github.hubspot.com/pace/docs/welcome/)
* [Heroku-style Loading Indicator](https://gist.github.com/patientdev/3dac07a069713c33d4d4cc039aa5ac2d)
* [react-flexview](https://github.com/buildo/react-flexview)
* [react-x-ray - CSS Layout Debugger](https://github.com/jxnblk/react-x-ray)

```js
import React from 'react';

export default class HerokuLoadingIndicator extends React.Component {
    constructor() {
        super();
        const GLYPHS = [
            '\u28FE', // ⣾
            '\u28FD', // ⣽
            '\u28FB', // ⣻
            '\u28BF', // ⢿
            '\u287F', // ⡿
            '\u28DF', // ⣟
            '\u28EF', // ⣯
            '\u28F7'  // ⣷
        ];
        this.state = {
            glyphs_index: 0,
            glyphs: GLYPHS
        };
    }

    // After the component mounts, cycle through the glyphs.
    componentDidMount() {
        this.timerID = setInterval(
            () => this.updateGlyphsIndex(),
            75
        );
    }

    // Before the component unmounts, stop cycling the glyphs.
    componentWillUnmount() {
        clearInterval(this.timerID);
    }

    // Move to the next glyph. Uses modular arithmetic to cycle through the glyphs.
    updateGlyphsIndex() {
        this.setState((prevState) => ({
            glyphs_index: (prevState.glyphs_index + 1) % this.state.glyphs.length
        }));
    }

    render() {
        return (
            <span className="heroku-loading-indicator">
                {this.state.glyphs[this.state.glyphs_index]}
            </span>
        );
    }
}

```

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
* [ExtReact](https://www.sencha.com/products/extreact/#app)
* [Microsoft Office UI Fabric](https://dev.office.com/fabric#/components) Also see [Repo](https://github.com/OfficeDev/office-ui-fabric-react) and [Components](https://developer.microsoft.com/en-us/fabric#/components)
* [**Pivotal**](https://styleguide.pivotal.io/)
* [Material-UI](http://www.material-ui.com/#/)
* [Khan Academy](https://khan.github.io/react-components/)
* [Search reusable React components](http://www.reactjsx.com/)
* [Another search engine for components](https://devarchy.com/react)

## Blank Slate

* [react-skeletor](https://github.com/trainline/react-skeletor)

## Case Study

* [react-soundplayer](http://labs.voronianski.com/react-soundplayer/)
* [react-aria](https://github.com/souporserious/react-aria)

## PDF

* [Rendering PDFs with React Components](https://themeteorchef.com/tutorials/rendering-pdfs-with-react-components)
* [react-pdf - Display PDF using pdf.js with worker](https://github.com/wojtekmaj/react-pdf)
* [react-pdf](https://github.com/diegomura/react-pdf)

## Table (Filtering, Pagination)

> Tables are effective because the nature of enterprise applications requires users to view rows of data simultaneously, scanning through alerts, comparing data and looking at data in any specific order of the user's choice.
> 
> What you are seeing below might seem like a very regular table pattern and might seem like there is nothing wrong about the usability of it at first, but as you get deeper into working on it, one would start realizing the quirks of operating it.

When paging, you can use arrow key. We also need to buffer and throttle requests

If there are only 2 or 3 pages worth of data, why not just show all?

* [Introducing react-pivottable](https://codeburst.io/introducing-react-pivottable-4bfdd511afed)
* [preact-virtual-list](https://github.com/developit/preact-virtual-list)
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
* [Use HOC for pagination, sorting, etc.](https://codebrahma.com/using-higher-order-components-react-application/)
* [Griddle - An ultra customizable datagrid](https://griddlegriddle.github.io/Griddle/)

## Spreadsheet

* [Handsontable](https://handsontable.com/)
* [currency.js](https://github.com/scurker/currency.js)

## Show/Hide

* [render-if](https://github.com/ajwhite/render-if)
* [react-only-if](https://github.com/MicheleBertoli/react-only-if)
* [react-hoverbox](https://github.com/wix/react-hoverbox)
* [react-detect-offline - Render certain content only when online (or only when offline)](https://github.com/chrisbolin/react-detect-offline)
* [Accessible W3C conform accordion written in ES6](https://oncode.github.io/handorgel/)

## Modal and Dialog

* [react-portal](https://github.com/tajo/react-portal)
* [react-slot-fill](https://github.com/camwest/react-slot-fill)
* [react-waypoint](https://github.com/brigade/react-waypoint)
* [react-accessible-modal](https://github.com/springload/react-accessible-modal)
* [react-poppop](https://ctxhou.github.io/react-poppop/)

## Panel, Window

* [react-mosaic](https://github.com/palantir/react-mosaic)
* [resize.js](https://github.com/no-stack-dub-sack/cs-playground-react/blob/master/src/utils/resize.js)
* [simpledrag](https://github.com/lingtalfi/simpledrag)

## Menu

* [react-contexify](https://github.com/fkhadra/react-contexify)

## Tree View

* [bosket](https://elbywan.github.io/bosket/)

## Auto-complete and Instant Search

* [**Downshift**](https://medium.com/@kentcdodds/introducing-downshift-for-react-b1de3fca0817)
* [downshift](https://github.com/paypal/downshift)
* [RDropdown](https://github.com/jamhall/rdropdown)
* [GooglePlaceAutocomplete](https://github.com/ydeshayes/googlePlaceAutocomplete)
* [Algolia](https://community.algolia.com/react-instantsearch/)
* [react-categorized-tag-input](http://erizocosmi.co/react-categorized-tag-input/)

```js
import debounce from 'lodash/debounce'

class Projects extends Component {
  state = {
    projects: fakeProjects,
    value: ''
  }
  
  handleFilter = debounce((e) => {
    this.setState(/* whatever */)
  }, 500)
}
```

## Keyboard and Mouse

* [react-combo-keys](https://github.com/SamyPesse/react-combo-keys)

## Scroll

* [Build a Reusable Scroll View Component with Animated scrollTo Abilities in React](https://codedaily.io/screencasts/48/Build-a-Reusable-Scroll-View-Component-with-Animated-scrollTo-Abilities-in-React)
* [scroll-into-view](https://github.com/KoryNunn/scroll-into-view)
* [Scrollytelling with IntersectionObserver](https://github.com/russellgoldenberg/scrollama)

## Date Picker and Calendar

* [Making input type=date complicated](https://medium.com/samsung-internet-dev/making-input-type-date-complicated-a544fd27c45a)
* [Designing The Perfect Date And Time Picker](https://www.smashingmagazine.com/2017/07/designing-perfect-date-time-picker/)
* [react-big-calendar](https://github.com/intljusticemission/react-big-calendar)
* [react-calendar-timeline](https://github.com/namespace-ee/react-calendar-timeline)
* [react-dates from Airbnb](https://github.com/airbnb/react-dates)
* [react-day-picker](http://react-day-picker.js.org)
* [calreact](https://github.com/learnetto/calreact)
* [spectre](https://picturepan2.github.io/spectre/experimentals.html#calendars)
* [react-date-picker](https://github.com/wojtekmaj/react-date-picker)

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
* [How To Make A Drag-and-Drop File Uploader With Vanilla JavaScript](https://www.smashingmagazine.com/2018/01/drag-drop-file-uploader-vanilla-js/)

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
* [tab-container-component](https://github.com/plantain-00/tab-container-component)
* [react-multistep](https://github.com/srdjan/react-multistep)

```html
<Tabs>
  <TabList>
    <Tab>Tacos</Tab>
    <Tab disabled>Burritos</Tab>
    <Tab>Coconut Korma</Tab>
  </TabList>
  <TabPanels>
    <TabPanel><p>Tacos are delicious</p></TabPanel>
    <TabPanel><p>Burritos are bad</p></TabPanel>
    <TabPanel><p>Coconut Korma is nice</p></TabPanel>
  </TabPanels>
</Tabs>
```

You will want to use implicit props to pass down information on which `<Tab>` and `<TabPanel>` to be selected.

```js
// We do not want to do this to use a props because we want
// <Tab> to manage the state entirely in silent
<TabPanels activeIndex={2}>
</TabPanels>
```

```js
class Tabs extend Component {
  state = {
    // Keep track of which tab is active
    activeIndex: 1
  }
  
  render() {
    // We map over children and give each child component
    // additional implicit props on the state managed by
    // this <Tab>
    const children = React.Children.map(this.props.children, (child) => {
      return React.cloneElement(child, {
        activeIndex: this.state.activeIndex
      })
    })
    
    return (
      <div className="tabs">
        {children}
      </div>
    )
  }
}
```

We can also use context instead of `React.Children.map`:

```js
class Tabs extend Component {
  static childContextTypes = {
    activeIndex: PropTypes.number.isRequired,
    onSelectTab: PropTypes.func.isRequired,
  }

  state = {
    activeIndex: 0
  }
  
  getChildContext() {
    return {
      activeIndex: this.state.activeIndex,
      onSelectTab: this.selectTabIndex
    }
  }
  
  render() {
    return (
      <div className="tabs">
        {this.props.children}
      </div>
    )
  }
}
```

## Sortable and Drag and Drop

* [Some react-dnd example](https://gist.github.com/krzysu/1b391ae0e3c87d0c654cdf6d5a409632)
* [Rethinking drag and drop](https://medium.com/@alexandereardon/rethinking-drag-and-drop-d9f5770b4e6b)
* [Shopify Draggable](https://shopify.github.io/draggable/)
* [react-beautiful-dnd by Atlassian](https://github.com/atlassian/react-beautiful-dnd)
* [Dragging React performance forward](https://medium.com/@alexandereardon/dragging-react-performance-forward-688b30d40a33)

## D3 and Charts

* [A starting point on using D3 with React](https://blog.sicara.com/a-starting-point-on-using-d3-with-react-869fdf3dfaf#.aood1myab)
* [Nivo](http://nivo.rocks/#/)
* [Chartify](https://kis.github.io/chartify/)

## Images

* [css-aspect-ratio](https://github.com/sgomes/css-aspect-ratio)
* [Low Quality Image Placeholders (LQIP) for Webpack](https://github.com/zouhir/lqip-loader)

## Editor

* [Learn DraftJS](https://learn-draftjs.now.sh/)
* [Dante 2](https://michelson.github.io/dante2/)
* [Slate](https://github.com/ianstormtaylor/slate)
* [react-in-markdown](https://github.com/kitze/react-in-markdown)
* [markdown-it](https://github.com/markdown-it/markdown-it)
* [react-mde - React Markdown Editor](https://github.com/andrerpena/react-mde)
* [Anchorme - Tiny, fast, efficient, feature rich Javascript library to detect links/URLs/Emails in text and convert them to clickable HTML anchor links](https://alexcorvi.github.io/anchorme.js/)
* [Alloy Editor](http://alloyeditor.com/)
* [Creating a rich text editor - Part 1 - Barebones Editor](http://bitwiser.in/2017/04/11/creating-rte-barebones-editor.html)
* [Draft-js building search and replace functionality](https://medium.com/@juliandoesstuff/draft-js-building-search-and-replace-functionality-688fd84f64cb)
* [ProseMirror](http://prosemirror.net/)
* [CKEditor 5: A new era for rich text editing](https://ckeditor.com/blog/CKEditor-5-A-new-era-for-rich-text-editing/)
* [draft-regex](https://github.com/YozhikM/draft-regex)

