# Reusable multicasting with Subject factories
[Video](https://egghead.io/lessons/rxjs-reusable-multicasting-with-subject-factories)

Passing a **subject factory** into ``multicast`` allows us to restart a shared execution that had already completed.

```js
const subjectFactory = () => new Rx.Subject()

const sharedObservable = Rx.Observable
  .interval(1000).take(5)
  .multicast(subjectFactory)
  .refCount()

const observerA = {
  next: x => console.log(`A next ${x}`),
  error: err => console.log(`A error ${err}`),
  complete: () => console.log('A done'),
}

let subA = sharedObservable.subscribe(observerA) // start shared execution

const observerB = {
  next: x => console.log(`B next ${x}`),
  error: err => console.log(`B error ${err}`),
  complete: () => console.log('B done'),
}

let subB
setTimeout(() => subB = sharedObservable.subscribe(observerB), 2000)

setTimout(() => {
  subA.unsubscribe()
  subB.unsubscribe() // stop shared execution
}, 5000)

setTimout(() => {
   subA = sharedObservable.subscribe(observerA) // restart shared execution with a new subject
}, 7000)
```
