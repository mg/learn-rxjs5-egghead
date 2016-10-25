# Combination operator: combineLatest
[Video](https://egghead.io/lessons/rxjs-combination-operator-combinelatest)

- ``combineLatest`` is the **AND** operator of RxJS.
- Combine **N** streams into **1** resulting stream.
- Combination function takes in **N** parameters and returns **1** value.
- On each invocations, the function receives the newest value from the stream that just emitted and the latest value from all the other stream.
- Useful if you have N **independent** sources of values, and you want to combine them in a logical way.
- It is an **AND** operation in the sense that the resulting stream of values are dependent on values from all the underlying streams.

```js
/*
foo:  ----0----1----2----(3|)
bar:  --0--1--2--3--(4|)
        combineLatest((x,y) =>x+y)
baz:  ----01--23-4--(56)-(7|)
*/
const foo = Rx.Observable.interval(500).take(4)
const bar = Rx.Observable.interval(300).take(5)
const baz = foo.combineLatest(bar, (x,y) =>x+y)
const bam == Rx.Observable.combineLatest(foo, bar, (x,y) =>x+y)
```
