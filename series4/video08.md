# Use RxJS mergeMap for fine-grain custom behavior
[Video](https://egghead.io/lessons/rxjs-use-rxjs-mergemap-for-fine-grain-custom-behavior)

Almost any operator in Rx can be rewritten as a ``mergeMap`` or a ``switchMap``.

```js
const source$ = Rx.Observable.intreval(500).take(5)

/*
---0---1---2---3---4|

map
---0--10--20--30--40|

mergeMap
---+---+---+---+---+|
   \   \   \   \   \
   0|  10| 20| 30| 40|

---0--10--20--30--40|
*/

const result1$ = source$
  .map(x => 10 * x)

const result2$ = source$
  .mergeMap(x => Rx.Observable.of(10 *x))

/*
---0---1---2---3---4|

filter
---0-------2-------4|

mergeMap
---+---+---+---+---+|
   \   \   \   \   \
   0|  |   2|  |   4|
---0-------2-------4|
*/

const result3$ = source$
  .filter(x => x % 2 === 0)

const result4$ = source$
  .mergeMap(x => {
    if(x % 2 === 0) {
      return Rx.Observable.of(x)
    } else {
      return Rx.Observable.empty()
    }
  })
```
