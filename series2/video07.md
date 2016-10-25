# Filtering operators: takeLast, last, skipLast
[Video](https://egghead.io/lessons/rxjs-filtering-operators-takelast-last)

Operators ``take``, ``first`` and ``skip`` refer to the **beginning** of a stream. ``takeLast``, ``last`` and ``skipLast`` refer to the **ending** of a stream.

Once a stream ends, the operators will emit the last values synchronously.  

```js
/*
foo: ---0---1---2---3---4---5---6---7---...
        take(5)
     ---0---1---2---3---(4|)
        takeLast(2)
bar: --------------------(34|)
*/
const foo = Rx.Observable.interval(1000).take(5)
const bar = foo.takeLast(2)

/*
foo: ---0---1---2---3---4---5---6---7---...
        take(5)
     ---0---1---2---3---4|    
        last()
baz: ------------------(4|)
*/
const baz = foo.last()

/*
foo: ---0---1---2---3---4---5---6---7---...
        take(5)
     ---0---1---2---3---(4|)  
        skipLast(2)
bam: -----------0---1---(2|)
*/
const bam = foo.skipLast(3)
```
