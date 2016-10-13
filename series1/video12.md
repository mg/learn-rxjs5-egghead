# Returning subscriptions from the subscribe function
[Video](https://egghead.io/lessons/rxjs-returning-subscriptions-from-the-subscribe-function)

Use unsubscribe function to clean up resources.

```js
const subscribe = observer => {
  // call things on observer
  const id = setInterval(() => observer.next('hi'), 1000)
  // return unsubscribe function
  return () {
    // clean up resources, such as intervals
    clearInterval(id)
  }
}

const foo = Rx.Observable(subscribe)

const subscription = foo.subscribe(v => console.log(v))

setTimeout(() => subscription.unsubscribe(), 5000)
```
