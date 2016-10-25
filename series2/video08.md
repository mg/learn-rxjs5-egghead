# Combination operators: concat, startWith
[Video](https://egghead.io/lessons/rxjs-combination-operators-concat-startwith)

Concat only works with finite observables (except the last one added).

```js
/*
foo:  ---0---1---2---3---4---5---6---7---...
         take(4)
      ---0---1---2---(3|)
more: (456789|)
         concat
bar:  ---0---1---2---(3456789)|
*/
const foo = Rx.Observable.interval(1000).take(4)
const more = Rx.Observable.of(4,5,6,7,8,9)
const bar = foo.concat(more)
const baz = Observable.concat(foo, more) // same as above

/*
foo:  ---0---1---2---3---4---5---6---7---...
       startWith('a')
bam:  a--0---1---2---3---4---5---6---7---...
*/
const bam = Rx.Observable.interval(1000).startWith('a')
```
