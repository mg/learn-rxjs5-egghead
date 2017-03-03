# Flatten a higher order observable with mergeAll in RxJS
[Video](https://egghead.io/lessons/rxjs-flatten-a-higher-order-observable-with-mergeall-in-rxjs)

#### Merging all inner observables concurrently
``mergeAll(n)`` will keep all inner observables running and merge the outputs together. Argument **n** is optional and if supplied, **mergeAll** will only allow **n** observables to run at the same time; when a new one is added it will not be subscribed to if **n** observables are already running.

```js
/*
------+---------+---------
      \         \
       -0-1-2-3  -0-1-2-3

       mergeAll

--------0-1-2-3-4-0516273-
*/

const click$ = Rx.Observable.fromEvent(document, 'click')
const clock$ = click$
  .map(click => Rx.Observable.interval(1000))
  .mergeAll()

clock$.subscribe(x => console.log(x))
```
