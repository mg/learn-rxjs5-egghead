# Observables are almost like Functions
[Video](https://egghead.io/lessons/rxjs-observables-are-almost-like-functions)


Observable is not an emitter, but a powerful version of a function.
- The contents of an observable is **lazy** and won't run unless called.
- Both are **synchronous**.
- Major difference is a function can return only once, but an observable can call **next()** as often as needed.
- Also, we can call **async** code inside an observable body, and this code will be async with respect to the caller.

```js
function foo() {
  // lazy, will not execute until foo() is called
  console.log('Hello')
  return 42
}

console.log('a')
console.log(foo.call())
console.log('b')

// outputs:
// a
// Hello
// 42
// b

const bar = Rx.Observable.create(observer => {
  // lazy, will not execute until subscribed to
  console.log('Hello')
  observer.next(42)
})

console.log('a')
bar.subscribe(x => console.log(x))
console.log('b')

// outputs:
// a
// Hello
// 42
// b
```
