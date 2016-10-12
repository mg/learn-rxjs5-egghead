# Creation operator: of()
[Video](https://egghead.io/lessons/rxjs-creation-operator-of)

Documentation of observables: http://reactivex.io/documentation/operators.html

Creation operators are essentially static functions on the **Observable** type:
- ``Rx.Observable.of``
- ``Rx.Observable.from``
- ``Rx.Observable.create``

####

```js
// this observable
const foo = Rx.Observable.create(observer => {
  observer.next(1)
  observer.next(2)
  observer.next(3)
  observer.complete()
})

// can be created with of()
const bar = Rx.Observable.of(1,2,3)
```
