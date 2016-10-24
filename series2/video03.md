# Transformation operator: map and mapTo
[Video](https://egghead.io/lessons/rxjs-transformation-operator-map-and-mapto)

```js
/*
foo: ---0---1---2---3---4---...
        map(v => v*2)
bar: ---0---2---4---6---8---...
*/
const foo = Rx.Observable.interval(1000)
const bar = foo.map(v => v * 2)

/*
foo: ---0---1---2---3---4---...
        mapTo(4)
baz: ---4---4---4---4---4---...
*/
const foo = Rx.Observable.interval(1000)
const baz = foo.mapTo(4)

```
