# Observables can complete
[Video](https://egghead.io/lessons/rxjs-observables-can-complete)

Completing is important for many functions, e.g. to concatenate two observables, the second can only start after the first one has completed (otherwise, we are merging not concatenating).
```js
const bar = Rx.Observable.create(observer => {
  try {
    console.log('Hello')
    observer.next(42)
    observer.complete()
  } catch(e) {
    observer.error(e)    
  }
})

console.log('a')
bar.subscribe({
  x => console.log(x),          // next handler
  error => console.log(error),  // error handler
  () => console.log('done'),    // complete handler
})
console.log('b')
```
