# Combination operator: merge
[Video](https://egghead.io/lessons/rxjs-combination-operator-merge)

``merge`` is the **OR** operator of RxJS.

```js
/*
foo:  ----0----1----2----(3|)
bar:  --0--1--2--3--(4|)
        merge
baz:  --0-01--21-3--(24)-(3|)
*/
const foo = Rx.Observable.interval(500).take(4)
const bar = Rx.Observable.interval(300).take(5)
const baz = foo.merge(bar)
const bam == Rx.Observable.merge(foo, bar)
```
