# Libraries

https://github.com/sindresorhus/modern-normalize

**https://inclusive-components.design/**

> Look at **jQuery UI** or **YUI** for props and widgets inspiration? - [Compound Components](https://www.youtube.com/watch?v=hEGg-3pIHlE)

https://github.com/hsnaydd/moveTo/

https://dollarshaveclub.github.io/stickybits/

* [200+ components](https://www.javascriptstuff.com/react-components/)
* [**JS.Coach**](https://js.coach/)
* [**Awesome React Components & Libraries**](https://github.com/brillout/awesome-react-components)
* [React Desktop](http://reactdesktop.js.org/)
* [Best Practices on building a UI component library for your company](https://www.youtube.com/watch?v=j8eBXGPl_5E)
* [CUID compared to UUID or shortid](https://github.com/ericelliott/cuid)
* [reflective-bind](https://github.com/flexport/reflective-bind)
* [insane - Lean and configurable whitelist-oriented HTML sanitizer](https://www.npmjs.com/package/insane)
* [passw0rd](https://github.com/djadmin/passw0rd)
* [ow - Function argument validation for humans](https://github.com/sindresorhus/ow)
* [A guide to building a React component with webpack 4, publishing to npm, and deploying the demo to GitHub Pages](https://medium.com/dailyjs/building-a-react-component-with-webpack-publish-to-npm-deploy-to-github-guide-6927f60b3220)
* [11 Javascript Utility Libraries You Should Know In 2018](https://blog.bitsrc.io/11-javascript-utility-libraries-you-should-know-in-2018-3646fb31ade)

https://github.com/jaredpalmer/react-fns

## A11Y

* [Accessibility auditing for React.js applications](https://github.com/dequelabs/react-axe)

## Toggle

* [react-toggled](https://github.com/kentcdodds/react-toggled)
* [Some toggle example](https://jrsinclair.com/articles/2018/react-redux-javascript-architecture/)
* [On Designing and Building Toggle Switches](https://www.sarasoueidan.com/blog/toggle-switch-design/)

## Breadcrumb

* [Build a Stunning Breadcrumb Component in React with Plain CSS](https://medium.com/better-programming/build-a-stunning-breadcrumb-component-in-react-with-plain-css-414c68db293)

## Visual

* [React Color](https://casesandberg.github.io/react-color/)
* [Pure CSS Tooltips](https://medium.freecodecamp.org/a-step-by-step-guide-to-making-pure-css-tooltips-3d5a3e237346)
* [Popper.js](https://popper.js.org/)
* [Pace.js - For loading](http://github.hubspot.com/pace/docs/welcome/)
* [Heroku-style Loading Indicator](https://gist.github.com/patientdev/3dac07a069713c33d4d4cc039aa5ac2d)
* [react-flexview](https://github.com/buildo/react-flexview)
* [react-x-ray - CSS Layout Debugger](https://github.com/jxnblk/react-x-ray)
* [react-content-loader](http://danilowoz.com/react-content-loader/)
* [react-measurements](https://github.com/rmfisher/react-measurements)
* [vanilla-tilt.js](https://micku7zu.github.io/vanilla-tilt.js/)
* [react-three-fiber](https://github.com/drcmda/react-three-fiber)

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

## Utilities

* [Voca is a JavaScript library for manipulating strings](https://github.com/panzerdp/voca)
* [Mout - Modular JavaScript Utilities](https://github.com/mout/mout)
* [Convenient and dependency free wrapper for working with arrays and objects](https://github.com/ecrmnn/collect.js/)
* [lazy.js - Like Underscore, but lazier](https://github.com/dtao/lazy.js)
* [decimal.js](https://github.com/MikeMcl/decimal.js/)
* [The Platform](https://github.com/palmerhq/the-platform)
* [flopflip - Toggle features and ship software more often](https://github.com/tdeekens/flopflip)
* [fpsmeter](https://github.com/Darsain/fpsmeter)

## UI Libraries

* [iOS HIG](https://developer.apple.com/ios/human-interface-guidelines/resources/)
* [instructure-ui](https://instructure.github.io/instructure-ui/)
* [Semantic UI React](https://react.semantic-ui.com/introduction)
* [Ant Design of React](https://ant.design/docs/react/introduce)
* [Wix Style - React](https://github.com/wix/wix-style-react)
* [react-primitives](https://github.com/lelandrichardson/react-primitives)
* [Blueprint](http://blueprintjs.com/)
* [buffer-components](https://github.com/bufferapp/buffer-components)
* [ExtReact](https://www.sencha.com/products/extreact/#app)
* [Microsoft Office UI Fabric](https://dev.office.com/fabric#/components) Also see [Repo](https://github.com/OfficeDev/office-ui-fabric-react) and [Components](https://developer.microsoft.com/en-us/fabric#/components)
* [**Pivotal**](https://styleguide.pivotal.io/)
* [Material-UI](http://www.material-ui.com/#/)
* [Search reusable React components](http://www.reactjsx.com/)
* [Pinterest Gestalt](https://github.com/pinterest/gestalt)
* [Zendesk Garden](https://garden.zendesk.com/react-components/#!/Button/5)
* [Netlify](http://serverless-ux.netlify.com/)
* [Atlaskit](http://atlaskit.atlassian.com/packages)
* [Reakit](https://reakit.io/components/)
* [Evergreen](https://evergreen.segment.com/)

## Blank Slate

* [react-skeletor](https://github.com/trainline/react-skeletor)
* [react-content-loader](https://github.com/danilowoz/react-content-loader)

## Case Study

* [react-soundplayer](http://labs.voronianski.com/react-soundplayer/)
* [react-aria](https://github.com/souporserious/react-aria)

## PDF

* [Rendering PDFs with React Components](https://themeteorchef.com/tutorials/rendering-pdfs-with-react-components)
* [react-pdf - Display PDF using pdf.js with worker](https://github.com/wojtekmaj/react-pdf)
* [react-pdf](https://github.com/diegomura/react-pdf)
* [ReLaXed - Create PDF documents using web technologies](https://github.com/RelaxedJS/ReLaXed)
* [puppeteer-examples](https://github.com/GoogleChromeLabs/puppeteer-examples)

## Table (Filtering, Pagination, Datagrid)

* [Make a better budget with **Airtable** and the new web clipper block](https://blog.airtable.com/personal-budget-challenge/)
* [HTML Tables: All there is to know about them](https://medium.freecodecamp.org/html-tables-all-there-is-to-know-about-them-d1245980ef96)
* [react-pivot-table](https://www.syncfusion.com/react-ui-components/react-pivot-table)
* [The complete guide to building a smart data table in React](https://blog.logrocket.com/complete-guide-building-smart-data-table-react/)

```
<DataTable />
<InfoTable />
```

> Tables are effective because the nature of enterprise applications requires users to view rows of data simultaneously, scanning through alerts, comparing data and looking at data in any specific order of the user's choice.
> 
> What you are seeing below might seem like a very regular table pattern and might seem like there is nothing wrong about the usability of it at first, but as you get deeper into working on it, one would start realizing the quirks of operating it.

When paging, you can use arrow key. We also need to buffer and throttle requests

If there are only 2 or 3 pages worth of data, why not just show all?

* [Get started with React Grid in 5 minutes](https://medium.com/ag-grid/get-started-with-react-grid-in-5-minutes-f6e5fb16afa)
* [Shopify's new table component](https://www.shopify.com/partners/blog/polaris-update)
* [Introducing react-pivottable](https://codeburst.io/introducing-react-pivottable-4bfdd511afed)
* [preact-virtual-list](https://github.com/developit/preact-virtual-list)
* [sematable](https://github.com/sematext/sematable)
* [Facebook's fixed-data-table](https://github.com/facebook/fixed-data-table)
* [reactable](https://github.com/glittershark/reactable)
* [**react-table**](https://github.com/tannerlinsley/react-table)
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
* [Flexmonster - Pivot table](https://www.flexmonster.com/?r=m7)

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

* [How to use react context to create a modal](https://medium.com/@francesco.agnoletto/how-to-use-react-context-to-create-a-modal-d8a387e09c28)
* [react-portal](https://github.com/tajo/react-portal)
* [react-slot-fill](https://github.com/camwest/react-slot-fill)
* [react-waypoint](https://github.com/brigade/react-waypoint)
* [react-accessible-modal](https://github.com/springload/react-accessible-modal)
* [react-poppop](https://ctxhou.github.io/react-poppop/)

## Panel, Window

* [Nexus browser emulator - Window.js](https://gitlab.cern.ch/nexus-project/nexus-browser/blob/master/src/components/Window.js)
* [react-mosaic](https://github.com/palantir/react-mosaic)
* [resize.js](https://github.com/no-stack-dub-sack/cs-playground-react/blob/master/src/utils/resize.js)
* [simpledrag](https://github.com/lingtalfi/simpledrag)
* [nice-react-layout - Resizable panels](https://github.com/ekros/nice-react-layout)

## Menu

* [react-contexify](https://github.com/fkhadra/react-contexify)
* [All of GitHub's menus & dialogs work without JavaScript.](https://twitter.com/Keithamus/status/1098260366017134592/photo/1)

## Tree View

* [bosket](https://elbywan.github.io/bosket/)

## Auto-complete and Instant Search

* [autoComplete.js](https://github.com/TarekRaafat/autoComplete.js)
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
* [HotKeys.js](http://wangchujiang.com/hotkeys/)

## Scroll

* [Twitter - Infinite List and React](https://itsze.ro/blog/2017/04/09/infinite-list-and-react.html)
* [Twitter Lite](https://medium.com/@paularmstrong/twitter-lite-and-high-performance-react-progressive-web-apps-at-scale-d28a00e780a3)

```js
new IntersectionObserver(callback, options)
```

* [**Infinite component scrolling with React.lazy and IntersectionObserver**](https://itnext.io/infinite-component-scrolling-with-react-lazy-and-intersectionobserver-7774c03b08f2)
* [Build a Reusable Scroll View Component with Animated scrollTo Abilities in React](https://codedaily.io/screencasts/48/Build-a-Reusable-Scroll-View-Component-with-Animated-scrollTo-Abilities-in-React)
* [scroll-into-view](https://github.com/KoryNunn/scroll-into-view)
* [Scrollytelling with IntersectionObserver](https://github.com/russellgoldenberg/scrollama)
* [Infinite scroll techniques in React](https://blog.logrocket.com/infinite-scroll-techniques-in-react-adcfd7ff32bd)
* [Glide.js - slider and carousel](https://glidejs.com/docs/)
* [react-scroll-shadow](https://github.com/zzarcon/react-scroll-shadow)
* [react-virtualized](https://blog.logrocket.com/rendering-large-lists-with-react-virtualized-82741907a6b3)
* [react-window](https://react-window.now.sh)
* [Scroll Magic](http://scrollmagic.io/)

## Scrollbar

* [OverlayScrollbars](https://kingsora.github.io/OverlayScrollbars)
* [Two Browsers Walked Into a Scrollbar](https://www.filamentgroup.com/lab/scrollbars/)

## Date Picker and Calendar

https://www.unicode.org/reports/tr35/tr35-dates.html#Date_Field_Symbol_Table

---

* [timetable-fns](https://github.com/flightplan-tool/timetable-fns)
* [**react-day-picker**](http://react-day-picker.js.org/)
* [Create a custom calendar in React](https://blog.flowandform.agency/create-a-custom-calendar-in-react-3df1bfd0b728)
* [Day.js](https://github.com/xx45/dayjs)
* [InfiniteGrid's Calendar example](https://codepen.io/pen/)
* [Making input type=date complicated](https://medium.com/samsung-internet-dev/making-input-type-date-complicated-a544fd27c45a)
* [Designing The Perfect Date And Time Picker](https://www.smashingmagazine.com/2017/07/designing-perfect-date-time-picker/)
* [react-big-calendar](https://github.com/intljusticemission/react-big-calendar)
* [react-calendar-timeline](https://github.com/namespace-ee/react-calendar-timeline)
* [react-dates from Airbnb](https://github.com/airbnb/react-dates)
* [react-day-picker](http://react-day-picker.js.org)
* [calreact](https://github.com/learnetto/calreact)
* [spectre](https://picturepan2.github.io/spectre/experimentals.html#calendars)
* [react-date-picker](https://github.com/wojtekmaj/react-date-picker)
* [Date Range Picker](http://www.daterangepicker.com/)
* [A hunt for the perfect date picker UI](https://uxdesign.cc/date-picker-design-5c5ef8f35286)
* [TOAST UI Calendar](http://ui.toast.com/tui-calendar/)

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

* [Video on FileReader](https://www.youtube.com/watch?v=-AR-6X_98rM)
* [Drag and drop file upload](https://codepen.io/pixelass/pen/dpyBOd?editors=0010)
* [How To Make A Drag-and-Drop File Uploader With Vanilla JavaScript](https://www.smashingmagazine.com/2018/01/drag-drop-file-uploader-vanilla-js/)
* [Upload anything you throw at it](https://pqina.nl/filepond/)

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
* [React containers, some assembly required](https://medium.com/zendesk-engineering/react-containers-some-assembly-required-43dd54d879a8)

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

* [react-movable](https://github.com/tajo/react-movable)
* [What a Drag - Vojtech Miksu](https://www.youtube.com/watch?v=y_XkQ2qMTSA)
* [**Beautiful interactions**](https://medium.com/@alexandereardon/beautiful-interactions-8f67502ccf73)
* [Some react-dnd example](https://gist.github.com/krzysu/1b391ae0e3c87d0c654cdf6d5a409632)
* [Rethinking drag and drop](https://medium.com/@alexandereardon/rethinking-drag-and-drop-d9f5770b4e6b)
* [Shopify Draggable](https://shopify.github.io/draggable/)
* [react-beautiful-dnd by Atlassian](https://github.com/atlassian/react-beautiful-dnd)
* [Dragging React performance forward](https://medium.com/@alexandereardon/dragging-react-performance-forward-688b30d40a33)
* [Dragon Drop - Accessible drag and drop](https://github.com/schne324/dragon-drop)
* [selection.js - making visual DOM Selections](https://simonwep.github.io/selection/)
* [react-kanban](https://github.com/markusenglund/react-kanban)
* [smooth-dnd](https://github.com/kutlugsahin/smooth-dnd/)

## D3 and Charts

* [A starting point on using D3 with React](https://blog.sicara.com/a-starting-point-on-using-d3-with-react-869fdf3dfaf#.aood1myab)
* [**Nivo**](https://nivo.rocks/)
* [Chartify](https://kis.github.io/chartify/)
* [sparkline](https://github.com/fnando/sparkline)
* [chart-parts](https://github.com/Microsoft/chart-parts)
* [d3-funnel](https://jakezatecky.github.io/d3-funnel/)
* [Chart.js](https://github.com/chartjs/Chart.js)

## Images

* [css-aspect-ratio](https://github.com/sgomes/css-aspect-ratio)
* [Low Quality Image Placeholders (LQIP) for Webpack](https://github.com/zouhir/lqip-loader)

## Editor

* [Editor.js](https://github.com/codex-team/editor.js)
* [Slate JS](https://www.slatejs.org)
* [Learn DraftJS](https://learn-draftjs.now.sh/)
* [Dante 2](https://michelson.github.io/dante2/)
* [Slate](https://github.com/ianstormtaylor/slate)
* [react-in-markdown](https://github.com/kitze/react-in-markdown)
* [markdown-to-jsx](https://github.com/probablyup/markdown-to-jsx)
* [markdown-it](https://github.com/markdown-it/markdown-it)
* [react-mde - React Markdown Editor](https://github.com/andrerpena/react-mde)
* [Anchorme - Tiny, fast, efficient, feature rich Javascript library to detect links/URLs/Emails in text and convert them to clickable HTML anchor links](https://alexcorvi.github.io/anchorme.js/)
* [Alloy Editor](http://alloyeditor.com/)
* [Creating a rich text editor - Part 1 - Barebones Editor](http://bitwiser.in/2017/04/11/creating-rte-barebones-editor.html)
* [Draft-js building search and replace functionality](https://medium.com/@juliandoesstuff/draft-js-building-search-and-replace-functionality-688fd84f64cb)
* [ProseMirror](http://prosemirror.net/)
* [CKEditor 5: A new era for rich text editing](https://ckeditor.com/blog/CKEditor-5-A-new-era-for-rich-text-editing/)
* [draft-regex](https://github.com/YozhikM/draft-regex)
* [Let's build a fast, slick and customizable rich text editor with Slate.js and React](https://codeburst.io/lets-build-a-fast-slick-and-customizable-rich-text-editor-with-slate-and-react-part-ii-3d3908d89664)

