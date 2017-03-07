# Split an RxJS Observable into groups with groupBy
[Video](https://egghead.io/lessons/rxjs-group-higher-order-observables-with-rxjs-groupby)

``groupBy(groupFn: value => keyValue)``: Allows us to branch from a source observable base on some calculation on each value, sorting each value into a group where each group is an observable of a key value.

```js
const numbers$ = Rx.Observable.interval(500).take(5)

numbers$
  .groupBy(x => x % 2)
  .map(inner$ => inner$.count())
  .mergeAll()
  .subscribe(console.log)

/*
--0--1--2--3--4|

groupBy(x => x % 2)
--+--+
  \  \
  \  1-----3---|
  0-----2-----4|

map(inner$ => inner$.count())
--+--+
  \  \
  \  ---------2|
  ------------3|

mergeAll()
-------------(3,2)|
*/
```
