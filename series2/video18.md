# Filtering operators: distinct and distinctUntilChanged
[Video](https://egghead.io/lessons/rxjs-filtering-operators-distinct-and-distinctuntilchanged)

- ``distinct(?(a,b) => bool, ?Observable)``: Maintains an internal state of distinct values, only emitting a new value if it is not already in the registry. Takes an optional compare function to compare values (useful for e.g. normalizing on case). Another optional argument is an **flusher observable** witch signals when the internal registry should be cleared (e.g. Interval observable that fires every 30 seconds).

- ``distinctUntilChanged()``: Maintains a registry of only what happened last. Can be used as a **rate limiting** operator or a **filtering** function to avoid redundant events.

```js
/*
foo:  --a--b--a--c--(b|)
      distinct()
bar:  --a--b-----c--(b!)
*/
const foo = Rx.Observable.interval(500).take(5)
  .zip(Rx.Observable.of('a', 'b', 'a', 'c', 'b'), (x,y) => y)
const bar = foo.distinct()

/*
  --a--b--A--c--(b|)
      distinct((a,b) => a.toLowerCase() === b.toLowerCase())
  --a--b-----c--!
     distinct(undefined, flusher)
  --a--b--A--c--(b|)

*/
const flusher = Rx.Observable.interval(1100).take(1)
  .concat(Rx.Observable.never())

  /*
  foo:  --a--b--a--a--(b|)
        distinctUntilChanged()
  baz:  --a--b--a-----(b!)
  */

```
