# Multicasting shortcuts: publish() and variants
[Video](https://egghead.io/lessons/rxjs-multicasting-shortcuts-publish-and-variants)

- ``publish()``: A shortcut for ``multicast(new Rx.Subject())``.

- ``publishReplay(N, MS)``: A shortcut for ``multicast(new Rx.ReplaySubject(N, MS))``.

- ``publishBehavior(seed)``: A shortcut for ``multicast(new Rx.BehaviorSubject(seed))``.

- ``publishLast()``: A shortcut for ``multicast(new Rx.AsyncSubject())``.

- ``share()``: A shortcut for ``publish()`` + ``refCount()``

```js
const sharedObservable = Rx.Observable
  .interval(1000).take(5)
  .share()

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
