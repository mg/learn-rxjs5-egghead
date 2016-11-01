# RefCount: automatically staring and stopping an execution
[Video](https://egghead.io/lessons/rxjs-refcount-automatically-starting-and-stopping-an-execution)

A connected observable has an operator ``refCount`` that returns an observable of number of observers subscribed. It calls ``connect`` when first observer subscribes, and stops shared execution when last observer unsubscribes.

```js
// 0 => 1: connect
// 1 => 0: unsubscribe

const sharedObservable = Rx.Observable
  .interval(1000).take(5)
  .multicast(new Rx.Subject())
  .refCount()

const observerA = {
  next: x => console.log(`A next ${x}`),
  error: err => console.log(`A error ${err}`),
  complete: () => console.log('A done'),
}

const subA = sharedObservable.subscribe(observerA) // start shared execution

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
```
