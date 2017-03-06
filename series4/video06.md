# Use RxJS mergeMap to map and merge high order observables
[Video](https://egghead.io/lessons/rxjs-use-rxjs-mergemap-to-map-and-merge-high-order-observables)


#### From 1st order to higher order to 1st order in one operation
``mergeMap(mapFn, resultSelectFn, n)`` does ``map()`` and then ``mergeAll()``. Accepts **n** as an optional parameter, same as **mergeAll** did. Also accepts an optional result selector function (<outer>, <inner>) => <value>, where outer and inner are the values from the outer and inner observables respectively. **flatMap** is exactly the same as **mergeMap**.

```js
const click$ = Rx.Observable.fromEvent(document, 'click')

const performRequest = () =>
  fetch('https://mylocation/mydata')
    .then(res => res.json())

// only ever allow at most 3 requests to be running concurrently
const response$ = click$
  .mergeMap(click => performRequest(), (click, result) => result.email, 3)

response$.subscribe(console.log)
```
