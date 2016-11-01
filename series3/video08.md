# Stopping a shared observable execution
[Video](https://egghead.io/lessons/rxjs-stopping-a-shared-observable-execution)

Since a shared execution won't stop when the last observer unsubscribes, we need to save a reference to the subscription and manually unsubscribe.

```js
const connectableObservable = Rx.Observable
  .interval(1000).take(5)
  .multicast(new Rx.Subject())

const sub = connectableObservable.connect() // start shared execution

const observerA = {
  next: x => console.log(`A next ${x}`),
  error: err => console.log(`A error ${err}`),
  complete: () => console.log('A done'),
}

connectableObservable.subscribe(observerA)

const observerB = {
  next: x => console.log(`B next ${x}`),
  error: err => console.log(`B error ${err}`),
  complete: () => console.log('B done'),
}

setTimeout(() => connectableObservable.subscribe(observerB), 2000)

setTimout(() => {
  sub.unsubscribe() // stop shared execution and unsubscribe all observers
}, 5000)
```
