# BehaviorSubject: representing a value of time

**BehaviorSubject** always has a current value, either the last value observed or an initial value supplied on construction. Very useful to model **value-over-time** (e.g. your age) as opposed to an **event stream** (e.g. your birthday).

[Video](https://egghead.io/lessons/rxjs-behaviorsubject-representing-a-value-over-time)

####

```js
const subject = new Rx.BehaviorSubject(0)

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
0-----1---2---3-----------
A   0.1...2...3...........
B                  3.....
*/
```
