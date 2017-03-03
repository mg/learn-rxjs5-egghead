# Get started with higher order observables in RxJS

[Video](https://egghead.io/lessons/rxjs-get-started-with-higher-order-observables-in-rxjs)

#### Higher Order Observable
An observable that emits not values but observables.

```js
const num$ = Rx.Observable.interval(1000).take(4) // emits number values
const string$ = num$.map(x => `hello ${num}`) // emits string values
const hoo$ = num$.map(x => Rx.Observable.of(1,2)) // emits an observable of values

hoo$.subscribe(obs$ => obs$.subscribe(x => console.log(x)))
```

A more practical example
```js
const click$ = Rx.Observable.fromEvent(document, 'click')
const clock$ = click$.map(click => Rx.Observable.interval(1000))

// observe many tick streams, one for each click
clock$.subscribe(tick$ => tick$.subscribe(x => console.log(x)))
```
