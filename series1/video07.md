# Creation operators: from, fromArray, fromPromise
[Video](https://egghead.io/lessons/rxjs-creation-operators-from-fromarray-frompromise)

```js
// two are equivalent
const foo = Rx.Observable.of(1, 2, 3)
const bar = Rx.Observable.fromArray([1, 2, 3])

// subscribe to a promise
const baz = Rx.Observable.fromPromise(fetch('http://someurl.com'))

baz.subscribe({
  result => console.log(`result from someurl.com: ${result}`),
  error => console.log(`error from someurl.com: ${error}`),
  done => console.log('http request finished'),
})

// creates an observer from various types
let bez = Rx.Observable.from(arrayOrPromiseOrIteratorOrGenerator)
```

N.B. when creating an observable from a generator we are converting a pull based value into a push based value and all values are synchronously pulled from the generator and pushed to the subscriber.
