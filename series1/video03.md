# Observables (push) compared to generator functions (pull)
[Video](https://egghead.io/lessons/rxjs-observables-push-compared-to-generator-functions-pull)

- With generators, the **generator** is the **producer** of values, while the **consumer** is whoever calls next() on the genrator. With observables, the **Observable** is the **producer** while whoever subcrribes is the **consumer** of values.
- With observables, the producer determines when values are **pushed** while in a generator, the consumer determines when the values are **pulled**.
- **setInterval** makes sense inside a push based producer; since the producer is in control; but not in a pull based producer. In a pull relationship, **setInterval** belongs with the consumer.
- Generators are more useful as a passive factory of values.

```js
// Producer
function* baz() {
  console.log('Hello')
  yield 42
  yield 100
  yield 200
}

// Consumer
let iterator = baz()
console.log(iterator.next().value) // outputs "Hello"\n42
console.log(iterator.next().value) // ouptuts 100
console.log(iterator.next().value) // ouptuts 200
```
