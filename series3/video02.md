# Subject: an Observable and Observer hybrid

[Video](https://egghead.io/lessons/rxjs-subject-an-observable-and-observer-hybrid)

We want Observer A and Observer B see the same **execution** of the observable. The **Subject** is a hybrid construct, both an observable and observer. It has all the operators an observable has plus all the observer methods (``next``, ``error``, and ``complete``).

```js
const observable = Rx.Observable.interval(1000).take(5)

// const subject = new Rx.Subject()
const subject = {
  next: x => this.observers.forEach(o => o.next(x)),
  error: err => this.observers.forEach(o => o.error(err)),
  complete: () => this.observers.forEach(o => o.complete()),  
  observers: [],
  subscribe: observer => this.observers.push(o)
}

const observerA = {
  next: x => console.log(`A next ${x}`),
  error: err => console.log(`A error ${err}`),
  complete: () => console.log('A done'),
}

observable.subscribe(subject)
subject.subscribe(observerA)

const observerB = {
  next: x => console.log(`B next ${x}`),
  error: err => console.log(`B error ${err}`),
  complete: () => console.log('B done'),
}

setTimeout(() => subject.subscribe(observerB), 2000)
```
