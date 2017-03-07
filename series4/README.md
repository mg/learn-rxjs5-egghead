# Use Higher Order Observables in RxJS Effectively

##### Splitting: First Order Observable => Higher Order Observable
- ``map``: Map any value to an observable.
- ``window``: Split an observable based on another observable. See variants such as ``windowToggle`` and others.
- ``groupBy``: Split an observable base on a key value.

##### Flattening: Higher Order Observable -> First Order Observable
- ``switch``: Switch observables when next observable starts emitting.
- ``mergeAll``: Interleave parallel observables together into a single observable.
- ``concatAll``: Switch to next observable when current observable stops emitting.
- ``switchMap``: ``map`` + ``switch``.
- ``mergeMap``: ``map`` + ``mergeAll``.
- ``concatMap``: ``map`` + ``concatAll``.
