# Creation operator: create
[Video](https://egghead.io/lessons/rxjs-creation-operator-create)

Calling ``create()`` is the same as calling the constructor of the ``Rx.Observable`` type.

```js
// use constructor over create()
const subscribe = observer => {
  // observer is observer object with next, error, complete functions
}

const foo = new Rx.Observable(subscribe)

// use observer object
const observer = {
  next: v => console.log(v),
  error: err => console.log(err),
  complete: () => console.log('done'),  
}

// Observable.subscribe() is our subcribe() function that accepts an observer
foo.subscribe(observer)
```
