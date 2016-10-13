# Creation operators: interval and timer
[Video](https://egghead.io/lessons/rxjs-creation-operators-interval-and-timer)

- ``interval(period)``: Every **period** milliseconds deliver a value, starting at 0 and then incrementing by 1. Each observer that subscribes gets an isolated interval, each one starting at 0 and then incrementing.
- ``timer(startTime, period)``: Same as ``interval()`` but only start after ``startTime``, or if ``startTime`` is a ``Date()`` object, start at the specified date.

```js
const foo = Rx.Observable.interval(1000)

const bar = Rx.Observable.timer(3000, 1000)
```
