# Use RxJS switchMap to map and flatten higher order observables
[Video](https://egghead.io/lessons/rxjs-use-rxjs-switchmap-to-map-and-flatten-higher-order-observables)

#### From 1st order to higher order to 1st order in one operation
``switchMap()`` does ``map()`` and then ``switch()``. In one go we move to a higher order observable (map from a value to an observable) and switch back to a 1st order observable (flatten the observable back to a value). As a bonus, **switchMap** automatically converts a **Promise** to an **Observable**, so ``Rx.Observable.fromPromise`` is not needed inside **switchMap**.

```js
// Observable<Event> => Observable<number>

const click$ = Rx.Observable.fromEvent(document, 'click')
const clock$ = click$
  .switchMap(click => Rx.Observable.interval(1000).take(3)))
/*  
  same as
  Observable<Event> => Observable<Observable<Number>> => Observable<number>
  .map(click => Rx.Observable.interval(1000).take(3))
  .switch()
*/

clock$.subscribe(x => console.log(x))
```

**switchMap** is very commonly used with request/response from a server. If the user clicks more than once before server has responded, **switch** will automatically cancel previous requests.

```js
const performRequest = () =>
  fetch('https://mylocation/mydata')
    .then(res => res.json())

const response$ = click$
  .switchMap(click => performRequest())
  //.switchMap(click => Rx.Observable.fromPromise(performRequest()))

response$.subscribe(console.log)
```
