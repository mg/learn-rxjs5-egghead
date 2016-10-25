# Filtering operator: filter
[Video](https://egghead.io/lessons/rxjs-filtering-operator-filter)

```js
/*
foo: ---0---1---2---3---4---...
        filter(v => v%2 === 0)
bar: ---0-------2-------4---...
*/
const foo = Rx.Observable.interval(1000)
const bar = foo.filter(v => v % 2 === 0)
```
