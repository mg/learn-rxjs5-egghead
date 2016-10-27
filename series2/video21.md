# Transformation operator: repeat
[Video](https://egghead.io/lessons/rxjs-transformation-operator-repeat)

- ``repeat(?N)``: Repeat an observable **N** times or forever if **N** is omitted. Useful for creating observables from other observables that should have a repeated pattern.

```js
/*
foo:  --a--b--c--(d|)
      map()
      --A--B--C--(D|)
      repeat(3)
bar:  --A--B--C--D--A--B--C--D--A--B--C--(D|)
*/
const foo = Rx.Observable.interval(500).take(5)
  .zip(Rx.Observable.of('a', 'b', 'c', 'd'), (x,y) => y)
const bar = foo.map(x => x.toUpperCase()).repeat(3)
```
