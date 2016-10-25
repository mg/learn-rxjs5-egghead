# Filtering operators: take, first, skip
[Video](https://egghead.io/lessons/rxjs-filtering-operators-take-first-skip)

- ``take``: take N numbers and then stop
- ``first``: shortcut for take(1)
- ``skip``: ignore first N numbers

```js
/*
foo: ---0---1---2---3---4---...
        take(3)
bar: ---0---1---(2|)
*/
const foo = Rx.Observable.interval(1000)
const bar = foo.take(3)

/*
foo: ---0---1---2---3---4---...
        first()
baz: ---0|
*/
const baz = foo.first()

/*
foo: ---0---1---2---3---4---...
        skip(3)
bam: ---------------3---4---...
*/
const bam = foo.skip(3)
```
