# Combination operator: zip
[Video](https://egghead.io/lessons/rxjs-combination-operator-zip)

- An **AND** style operator.
- First value of foo and first value of bar is first value of stream
- Second value of foo and second value of bar is second value of stream

```js
/*
foo:  ----0----1----2----3----(4|)
bar:  ---0---1---2---(3!)
        zip((x,y) => x+y)
baz:  ----0----2----4----(6|)
*/
const foo = Rx.Observable.interval(500).take(5)
const bar = Rx.Observable.interval(400).take(4)
const baz = foo.zip(bar, (x,y) => x+y)
const bam == Rx.Observable.zip(foo, bar, (x,y) => x+y)
```
- Generally, ``combineLatest`` and ``withLatestFrom`` are more useful than ``zip``.
- Can be useful to spread out values from an synchronous stream

```js
/*
foo:  (hello|)
bar:  ---0---1---2---3---(4!)
        zip((x,y) => x)
baz:  ---h---e---l---l---(o|)
*/
const foo = Rx.Observable.of('h', 'e', 'l', 'l', 'o')
const bar = Rx.Observable.interval(400).take(5)
const baz = foo.zip(bar, (x,y) => x)
```
