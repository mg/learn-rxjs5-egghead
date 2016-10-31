# ReplaySubject: remembering events from the past

[Video](https://egghead.io/lessons/rxjs-replaysubject-remembering-events-from-the-past)

Replays last **N** events when an observer subscribes to the subject. Takes two parameters on construction: **N** for buffer size and **MS** for window size (e.g. the maximum amount of time to remember past events).

```js
const bufferSize = 2 // use Number.POSITIVE_INFINITY for an unbound buffer
const subject = new Rx.ReplaySubject(bufferSize)

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
subject.next(1)
subject.next(2)
subject.next(3)

setTimeout(() => subject.subscribe(observerB), 2000)

/*
------1---2---3-----------
A   ..1...2...3...........
B                  (23)...
*/
```

``ReplaySubject(1)`` is the same as ``BehaviorSubject()``, except there is no **initial** value. **ReplaySubject** also replays events EVEN if the observable has completed, **BehaviorSubject** does not.
