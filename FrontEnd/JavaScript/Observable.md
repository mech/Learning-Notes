# Observable

Promises can only resolve once:

```js
// https://www.youtube.com/watch?v=Qg1SvpIau6U
// We have a promise that try to handle click event and resolve it.
// But it can only resolve one time and that's it.
// If the button is clicked the 2nd time, nothing will happen.
var p1 = new Promise((resolve, reject) => {
  $('#btn').click(evt => {
    var className = evt.target.className
    if (/foobar/.test(className)) {
      resolve(className)
    } else {
      reject()
    }
  })
})

p1.then(className => console.log(className))
```

Since button can be clicked indefinitely and sort of like a stream of events, we need to use other kind of primitive to handle them. Enter Observable!

```js
var obsv = Rx.Observable.fromEvent(btn, 'click')

obsv
  .map(evt => evt.target.className)
  .filter(className => /foobar/.test(className))
  .distinctUntilChanged() // does not move on to next step unless it got changed
  .subscribe(data => {
    var className = data[1]
    console.log(className)
  })
```