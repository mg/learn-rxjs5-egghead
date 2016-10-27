# Filtering operators: throttle and throttleTime
[Video](https://egghead.io/lessons/rxjs-filtering-operators-throttle-and-throttletime)

**Throttle** is similar to **delay**, but is more of a **filtering** operation rather than a **transformation** operator.

- ``throttleTime(ms)``: A **rate limiting** operator like ``debounceTime()``, but works backwards. It first emits and then waits for **ms** until emitting again, dropping values that come in before the timeout, and emitting just the newest value.

- ``throttle(x => Observer)``: Similar to ``delay``.

```js
/*
foo:  --0--1--2--3--(4|)
      throttleTime(1000)
bar:  --0-----2----(4!)
*/
const foo = Rx.Observable.interval(500).take(5)
const bar = foo.throttleTime(1000)
```
