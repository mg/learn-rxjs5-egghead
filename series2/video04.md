# Utility operator: do
[Video](https://egghead.io/lessons/rxjs-utility-operator-do)
- The most important operator in the utility category.
- Executes a side effect on each element in observable.
- Return value is ignored.
- Does not trigger a subscription.
- Very useful for debugging streams.

```js
/*
foo: ---0---1---2---3---4---...
        do(v => console.log(v))
bar: ---0---1---2---3---4---...
*/
const foo = Rx.Observable.interval(1000)
const bar = foo.do(v => console.log(v))
```
