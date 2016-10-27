# Transformation operator: scan
[Video](https://egghead.io/lessons/rxjs-transformation-operator-scan)

Combination operators can be thought as **vertical** combination operators (since they compose marble diagrams vertically). Horizontal operators compose a single observable across time.

``scan`` is a horizontal composer that accumulates state in the **accumulator**. It works very well with other vertical composers such as ``merge`` .

```js
/*
foo:  ----0----1----2----3----(4|)
      scan((acc, x) => y, initial)
bar:  ----0----1----3----6----(10!)
*/
const foo = Rx.Observable.interval(500).take(5)
const bar = foo.scan((acc, x) => acc + x, 0)
```

Example click counter
```js
/*
  ----ev----ev----ev----ev----...
      map(ev => 1)
  ----1-----1-----1-----1-----...      
      scan((acc, x) => acc + x, 0)
  ----1-----2-----3-----4-----...
*/
```
