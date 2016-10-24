# Marble diagrams in ASCII form
[Video](https://egghead.io/lessons/rxjs-marble-diagrams-in-ascii-form)

```js
/*
a, then b, then c, then d, then done
---a----b----c------d-------------|

0, then 1, then 2, then 3, then error
---0----1------2------3-----------X
*/

// ---0---1---2---3---4---5--6---...
Rx.Observable.interval(1000)

// (1234)|
Rx.Observable.of(1,2,3,4)

/*
foo: ---0---1---2---3---4---...
        multiplyBy(2)
bar: ---0---2---4---6---8---...
*/
const foo = Rx.Observable.interval(1000)
const bar = foo.multiplyBy(2)
```
