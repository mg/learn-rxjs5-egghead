# Combination operator: withLatestFrom
[Video](https://egghead.io/lessons/rxjs-combination-operator-withlatestfrom)

- Works similarly to ``combineLatest``.
- Is also an **AND** operator.
- When the source stream recieves value, return a new value that is derived from this value and the latest values from combined stream.
- Essentially, the resulting stream is a **map** of the first stream influenced by values from other streams.

```js
/*
foo:  ----H----e----l----l----o|
bar:  --0--1--0--1--0--1--0--1-
        withLatestFrom()
baz:  ----h----e----L----L----o|
*/
// watching text input
const foo = Rx.Observable.from(document.getElementByID('inputbox'), 'keyup').map(ev => ev.charCode)

// stream of a series of 0's and 1's
let count = 0
const bar = Rx.Observable.interval(300).map(v => {
  count++
  return count %% 2 === 0 ? 0 : 1
})

const baz = foo.withLatestFrom(bar, (ch, toggle) => toggle === 0 ? ch.toLowerCase() : ch.toUpperCase())
```
