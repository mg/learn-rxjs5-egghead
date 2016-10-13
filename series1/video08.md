# Creation operators: fromEventPattern, fromEvent
[Video](https://egghead.io/lessons/rxjs-creation-operators-fromeventpattern-fromevent)

To work with any API that looks like ``addEventHandler(handler)`` and ``removeEventHandler(handler)`` use the ``fromEventPattern`` operator.
```js
const foo = Rx.Observable.fromEventPattern(
  handler => document.addEventListener('click', handler),
  handler => document.removeEventListener('click', handler),
)
```
Once ``foo`` is subscribed to, the event handler is added to the document.

Under the hood, ``fromEventPattern`` is implemented something like
```js
function fromEventPattern(add, remove) {
  return Rx.Observable.create({observer => {
    add(e => observer.next(e))
  })
}
```

Another operator, ``fromEvent``, is specialized to handle DOM events. Here is no need for a remove handler.
```js
const foo = Rx.Observable.fromEvent(document, 'click')
```
