# Observables can throw errors
[Video](https://egghead.io/lessons/rxjs-observables-can-throw-errors)

```js
const bar = Rx.Observable.create(observer => {
  try {
    console.log('Hello')
    observer.next(42)
  } catch(e) {
    observer.error(e)    
  }
})

console.log('a')
bar.subscribe({
  x => console.log(x),          // next handler
  error => console.log(error),  // error handler
})
console.log('b')
```
