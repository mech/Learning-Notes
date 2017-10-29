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

> Observables are a function that take an observer and return a unsubscribing function.

* [Learning Observable By Building Observable](https://medium.com/@benlesh/learning-observable-by-building-observable-d5da57405d87)

```js
// Observable is just a function that take an observer
function Observable(observer) {
  // This is the magical part
  const ds = new DataSource()
  
  ds.ondata = (e) => observer.next(e)
  ds.onerror = (err) => observer.error(err)
  ds.oncomplete = () => observer.complete()
  
  // That return an cleanup function
  return () => {
    ds.destroy()
  }
}
```

## RxJS

* [Netflix JavaScript Talks - RxJS + Redux + React = Amazing!](https://www.youtube.com/watch?v=AslncyG8whg)
* [What is RxJS? And Why You Should Know About It](https://news.thisdot.co/what-is-rxjs-and-why-you-should-know-about-it-2a5afe58cea)