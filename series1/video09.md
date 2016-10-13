# Creation operators: empty, never, throw
[Video](https://egghead.io/lessons/rxjs-creation-operators-empty-never-throw)

Seemingly useless operators that can never the less be quite useful in combinations with other observables.
- ``empty()``: An observable that returns **done** the moment someone subscribes.
- ``never()``: An observable that never returns anything, no value, error nor completion. Can be thought as an **infinite** observabel.
- ``throw()``: An observable that throws an error and nothing else.

```js
const foo = Rx.Observable.empty()
const bar = Rx.Observable.never()
const baz = Rx.Observable.throw(new Error('bla'))
```
