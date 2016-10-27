# Transformation operators: debounce and debounceTime
[Video](https://egghead.io/lessons/rxjs-transformation-operators-debounce-and-debouncetime)

- ``debounceTime()``: A **rate limiting** operator. When value comes from source observable, ``debounceTime`` waits for **ms**. If source observable emits **no new value** in that time, it emits the value. If the source observable emits a new value before the *debounce* has passed, ``debounceTime`` stores the new value, drops the old value, and resets the clock. Very useful when creating input boxes that perform auto requests on the server when user types. Comparable to ``delay()``.

- ``debounce(x => Observable)``: Use an observable to determine how we want to debounce. Comparable to ``delayWhen``.

```js
/*
foo:  --0--1--2--3--(4|)
      debounceTime(1000)
bar:  ------------------(4!)
*/
const foo = Rx.Observable.interval(500).take(5)
const bar = foo.debounceTime(1000)

/*
foo:  --0--1--2--3--(4|)
      debounce(x => Observable)
baz:  ---0--1--2--3--(4!)
*/
const baz = foo.debounce(x => Observable.interval(200).take(1))
```
