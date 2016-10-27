# Error handling operator: catch
[Video](https://egghead.io/lessons/rxjs-error-handling-operator-catch)

``catch`` allows us to replace an error with an observable. That observable could return a **fix value**, stop the process or anything else.

```js
/*
foo:  --a--b--c--d--(2|)
      map()
      --A--B--C--D--X
      catch(err => Z)
bar:  --A--B--C--D--(Z|)
      catch(err => |)
baz:  --A--B--C--D--|
      catch(err => ----...)
bam:  --A--B--C--D------...
*/
const foo = Rx.Observable.interval(500).take(5)
  .zip(Rx.Observable.of('a', 'b', 'c', 'd', 2), (x,y) => y)
const bar = foo.map(x => x.toUpperCase()).catch(error => Rx.Observable.of('Z'))
const baz = foo.map(x => x.toUpperCase()).catch(error => Rx.Observable.empty())
const bam = foo.map(x => x.toUpperCase()).catch(error => Rx.Observable.empty())
```

``catch`` can take an optional **output observable**. This observable is essentially the input observable until it threw an error. This allows us to implement a **retry** logic.
