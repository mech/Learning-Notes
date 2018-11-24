# JavaScript Date

* [The Definitive Guide to JavaScript Dates](https://flaviocopes.com/javascript-dates/)

```js
const WEEKDAYS = [0, 1, 2, 3, 4, 5, 6]
const WEEKDAYFORMAT = 'dd' // Su, Mo, Tu, We, Th, Fr, Sa

// Typically for "en" it fall on Sunday (0)
const firstDayOfWeek = moment.localeData().firstDayOfWeek()
```

## date-fns

* Immutable and pure FP
* Alternative to the chaining API seen in moment.js
* `date-fns/fp` and `lodash/fp`

## Moment

```js
const currentMonth = moment()
const nextMonth = currentMonth.clone()
nextMonth.add(1, 'month')

this.setState({
  currentMonth: nextMonth
})
```