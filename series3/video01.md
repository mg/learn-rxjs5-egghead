# An Observable execution may only one on Observer

[Video](https://egghead.io/lessons/rxjs-an-observable-execution-may-only-have-one-observer?course=rxjs-subjects-and-multicasting-operators)

Each **observable** execution has only one **observer**. When we **subscribe**, we are invoking an **execution** of the **observable** use an **observer**. Each **execution** created is isolated from other **executions**. **Subjects** allows many **observers** to observe a **observable** in a **shared executon**.

```js
const observable = Rx.Observable.interval(1000).take(5)

const observerA = {
  next: x => console.log(`A next ${x}`),
  error: err => console.log(`A error ${err}`),
  complete: () => console.log('A done'),
}

observable.subscribe(observerA) // create an execution

const observerB = {
  next: x => console.log(`B next ${x}`),
  error: err => console.log(`B error ${err}`),
  complete: () => console.log('B done'),
}

setTimeout(() => observable.subscribe(observerB), 2000) // isolated execution, starts a new interval
```
