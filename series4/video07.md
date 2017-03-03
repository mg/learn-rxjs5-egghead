# Use RxJS concatMap to map and concat high order observables
[Video](https://egghead.io/lessons/rxjs-use-rxjs-concatmap-to-map-and-concat-high-order-observables)


#### From 1st order to higher order to 1st order in one operation
``concatMap(mapFn, resultSelectFn)`` does ``map()`` and then ``concatAll()``. Same as ``mergeMap()`` where **n** is equal to **1**.

```js
const performRequest = () =>
  fetch('https://mylocation/mydata')
    .then(res => res.json())

// only ever allow 1 request to be running
const response$ = click$
  .concatMap(click => performRequest(), (click, result) => result.email)

response$.subscribe(console.log)
```
