# Connection operator: multicast and connect

[Video](https://egghead.io/lessons/rxjs-connection-operator-multicast-and-connect)

``multicast`` is a on operator on an **observable** that simplifies allowing multiple observers on a single observable. Transforms the observable into a **connected** observable, i.e. an observable that is backed by a **subject**. It has one extra method, ``connect``, that **connects** the observable to the backing **subject** and invokes the execution.

```js
const connectableObservable = Rx.Observable
  .interval(1000).take(5)
  .multicast(new Rx.Subject())

connectableObservable.connect()

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
```
