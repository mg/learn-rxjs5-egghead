# Split an RxJS observable conditionally with windowToggle
[Video](https://egghead.io/lessons/rxjs-split-an-rxjs-observable-conditionally-with-windowtoggle)

``windowToggle(open$, close$)``: Split the source observable when open observable emits, and close the section when the close observable emits.

```js
const clock$ = Rx.Observable.interval(1000)
const down$ = Rx.Observable.fromEvent(document, 'mousedown')
const up$ = Rx.Observable.fromEvent(document, 'mouseup')

// result1$ only emits while mouse button is held down
const result$ = clock$
  .windowToggle(down$, () => up$)
  .switch()

/*
--0--1--2--3--4--5--6--7--8--9-- clock$
----------D-------------D------- down$
-------------------U------------ up$

windowToggle
----------+-------------+-------
          \             \
           3--4--5-|     -8--9--

switch
-----------3--4--5--------8--9--
*/
```

N.b. could have used mergeAll instead of switch, because the differences are only present when dealing with concurrency.
