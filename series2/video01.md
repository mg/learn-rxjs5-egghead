# What RxJS operators are
[Video](https://egghead.io/lessons/rxjs-what-rxjs-operators-are?course=rxjs-beyond-the-basics-operators-in-depth)
- Functions attached to the Observable type on the form ``() => Observable``
- Operator is always immutable, e.g. source is always untouched.

```js
function multiplyBy(multiplier) {
  const source = this
  const result = Rx.Observable.create(observer => {
    source.subscribe(
      value => observer.next(value * multiplier),
      err => observer.error(err),
      () => observer.complete(),
    )
  })
  return result
}

Rx.Observable.prototype.multiplyBy = multiplyBy

const foo = Rx.Observable.of(1, 2, 3, 4, 5)
const bar = foo.multiplyBy(10)
bar.subscribe(v => console.log(v))
```
