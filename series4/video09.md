# Split an RxJS observable with window
[Video](https://egghead.io/lessons/rxjs-split-an-rxjs-observable-with-window)

``window(observable)``: An operator that take an 1st order observable and return a higher order observable by splitting the source observable.

```js
const click$ = Rx.Observable.fromEvent(document, 'click')
const clock$ = Rx.Observable.interval(1000)

const result1$ = clock$
  .window(click$)
  .switch()

const result2$ = clock$
  .window(click$)
  .switchMap(obs => obs.count())

/*
--0--1--2--3--4--5--6--7--8-- clock$
-------c-------c---c--------- click$

window
+------+-------+---+---------
\      \       \   \
 -0--1-|2--3--4|-5-|6--7--8--

switch
--0--1--2--3--4--5--6--7--8--

switchMap(obs => obs.count())
+------+-------+---+---------
\      \       \   \
 ------2--------3---1--------


map
---0--10--20--30--40|

mergeMap
---+---+---+---+---+|
   \   \   \   \   \
   0|  10| 20| 30| 40|

---0--10--20--30--40|
*/
```
