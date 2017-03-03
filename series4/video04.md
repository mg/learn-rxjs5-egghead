# Flatten a higher order observable with concatAll in RxJS
[Video](https://egghead.io/lessons/rxjs-flatten-a-higher-order-observable-with-concatall-in-rxjs)

#### Concatenating observables when the previous stops
``concatAll()`` is simply ``mergeAll(1)``, i.e. run only one observable at a time, and when one finishes start the next one.

```js
/*
------+---------+-+-------
      \         \        \
       -0-1-2-|  -0-1-2-| -0-1-2-|

       concatAll

--------0-1-2----0-1-2-0-1-2
*/

const click$ = Rx.Observable.fromEvent(document, 'click')
const clock$ = click$
  .map(click => Rx.Observable.interval(1000).take(3))
  .concatAll()

clock$.subscribe(x => console.log(x))
```
