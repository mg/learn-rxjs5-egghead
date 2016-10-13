An observable is a way to deliver values from a producer to a consumer where the producer is lazy. The observable is created with various creators, for example:
- ``Rx.Observable.create(observer)``
- ``Rx.Observable.of(v1, v2, v3, ...)``
- ``Rx.Observable.fromArray(arrya)``
- ``Rx.Observable.fromPromise(promise)``
- ``Rx.Observable.from()``
- ``Rx.Observable.fromEventPattern()``
- ``Rx.Observable.fromEvent()``
- ``Rx.Observable.empty()``
- ``Rx.Observable.never()``
- ``Rx.Observable.throw()``
- ``Rx.Observable.interval()``
- ``Rx.Observable.timer()``

The observer exposes three functions; ``next()``, ``error()``, and ``completed()`` that the observable uses to push various values and events to the observer. The observable returns an optional unsubscribe function to clean up any resources that it uses. 

The observable is the foundation type for the Rx **operators** that we use to compose complex asynchronous operations.
