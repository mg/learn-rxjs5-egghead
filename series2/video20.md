# Error handling operator: retry and retryWhen
[Video](https://egghead.io/lessons/rxjs-error-handling-operator-retry-and-retrywhen)

- ``retry(?N)``: Resubsribes to the input observable when it sees an error. If **N** is supplied, only resubscribes **N** times until throwing an error. This is very useful when retrying HTTP requests.

- ``retryWhen(ErrorObservable => Observable)``: Return an observable that says when we should retry. Also useful for server request when we don't want to retry immediately but let some time pass.

```js
/*
foo:  --a--b--c--d--(2|)
      map()
      --A--B--C--D--X
      retry()
bar:  --A--B--C--D----A--B--C--D-----A--B--C--D--X
*/
const foo = Rx.Observable.interval(500).take(5)
  .zip(Rx.Observable.of('a', 'b', 'c', 'd', 2), (x,y) => y)
const bar = foo.map(x => x.toUpperCase()).retry(2)

/*
foo:  --a--b--c--d--(2|)
      map()
      --A--B--C--D--X
      retryWhen()
erobs --------------e-----------------e
baz:  --A--B--C--D--------A--B--C--D--X
*/
const baz = foo.map(x => x.toUpperCase()).retryWhen(err => err.delay(1000))
```
