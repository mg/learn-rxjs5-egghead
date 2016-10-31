# AsyncSubject: representing a computation that yields a final value

[Video](https://egghead.io/lessons/rxjs-asyncsubject-representing-a-computation-that-yields-a-final-value)

- ``ReplaySubject``: Replays many, before or after completion.

- ``BehaviorSubject``: Replays one, only before completion.

- ``AsyncSubject``: Replays one, only if completed. Useful for heavy computations that result in a value that we don't want to repeat for every observer.

```js
const subject = new Rx.AsyncSubject()

const observerA = {
  next: x => console.log(`A next ${x}`),
  error: err => console.log(`A error ${err}`),
  complete: () => console.log('A done'),
}

subject.subscribe(observerA)

const observerB = {
  next: x => console.log(`B next ${x}`),
  error: err => console.log(`B error ${err}`),
  complete: () => console.log('B done'),
}

// manually control the observers
setTimeout(() => subject.next(1), 100)
setTimeout(() => subject.next(2), 200)
setTimeout(() => subject.next(3), 300)
setTimeout(() => subject.complete(), 350)

setTimeout(() => subject.subscribe(observerB), 400)

/*
------1---2---3--|
A   .............(3|)
B                     (3|)
*/
```
