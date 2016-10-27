# Transformation operators: delay and delayWhen
[Video](https://egghead.io/lessons/rxjs-transformation-operators-delay-and-delaywhen)

- ``delay(ms)``: Shifts in time, prepends the stream with specified **ms** value.

- ``delay(Date)`` Delay until **Date**, then emit.

- ``delayWhen(x => Observable))``: Delay dependent on **observable**.

```js
/*
foo:  ----0----1----2----3----(4|)
      delay(1000)
bar:  ---------0----1----2----3----(4!)
*/
const foo = Rx.Observable.interval(500).take(5)
const bar = foo.delay(1000)

/*
foo:  ----0----1----2----3----(4|)
      delayWhen(x => ----0|)
baz:  ----0-------1--------2----------3------------(4!)
*/
const baz = foo.delayWhen(x => Rx.Observable.interval(x*x*100).take(1))
```
