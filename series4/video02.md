# Flatten a higher order observable with RxJS switch
[Video](https://egghead.io/lessons/rxjs-flatten-a-higher-order-observable-with-rxjs-switch)

Not a good idea to subscribe in a subscribe; not very readable and possible leaks since we are not cleaning up the inner subscriptions. The solution is to use a flattening operator:

``Observable<Observable<T>> => Observable<T>``

#### Switching from one observable to the next when the next starts
``switch()`` is such a flattening operator that, when the underlying stream emits a new observable, **switch** unsubscribes the previous observable and switches to the new one.

```js
/*
------+---------+---------
      \         \
       -0-1-2-3  -0-1-2-3

               switch

--------0-1-2-3---0-1-2-3-
*/

const click$ = Rx.Observable.fromEvent(document, 'click')
const clock$ = click$
  .map(click => Rx.Observable.interval(1000))
  .switch()

clock$.subscribe(x => console.log(x))
```
