# Transformation operator: buffer
[Video](https://egghead.io/lessons/rxjs-transformation-operator-buffer)

A horizontal combination that allows us to group values together. Comes in following variants:
- ``buffer(closing observable)``: Buffer items until **closing observable** signals. The **closing obserable** might be e.g. an interval observable that fires every **ms**. This is the same as ``bufferTime(ms)``.

- ``bufferCount(n)``: buffer at most **N** items together. If stream closes before buffer is full, emits the partial buffer.

- ``bufferTime(ms)``: buffer for **ms** time and emit.

- ``bufferToggle``: More advanced, see docs.

- ``bufferWhen``: More advanced, see docs.

```js
/*
foo:  ------h------e------l------l------(o|)
      bufferCount(2)
bar:  ------------([h,e])-------([l,l])-([o]!)
*/
const foo =Rx.Observable.of('h', 'e', 'l', 'l', 'o')
  .zip(Rx.Observable.interval(600).take(5), (x, y) => x)

const bar = foo.buffer(2)
```
