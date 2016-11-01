# Multicast with a selector argument, as a sandbox
[Video](https://egghead.io/lessons/rxjs-multicast-with-a-selector-argument-as-a-sandbox)

When a **selector** is passed to a ``multicast()`` it returns a regular observable, not a connected observable. Creates a **sandbox** of a shared execution inside the **selector**. The **selector** returns a single observer that executes the shared execution context. The shared execution stops when the observer unsubscribes. We should use a selector when we are creating a diamond shaped dependency of observables:

```
input:    A
merge: Ba   Bb
return:   C    
```

```js
const subjectFactory = () => new Rx.Subject()

const selector = shared => {
  // sandbox
  const sharedDelayed = shared.delay(500)
  return shared.merge(sharedDelayed)
}

const result = Rx.Observable
  .interval(1000).take(6)
  .do(x => console.log(x))
  .map(x => Math.random())
  .multicast(subjectFactory, selector)

const sub = result.subscribe(x => console.log(x))

setTimout(() => {
  sub.unsubscribe() // stop shared execution
}, 5000)
```
