# RxJS Subjects and Multicasting Operators

###### When to use a subject
- When we map to a random number, and want two or more observables to see the same random numbers, we must use a Subject.
- Often we need some behavior for observers that arrive late.
- Anytime we want to have many observables observe the same observer.

##### Subjects:
- ``Subject()``
- ``BehaviorSubject(seed)``
- ``ReplaySubject(bufferSize, windowSize)``
- ``AsyncSubject()``

##### Multicasting:
- ``multicast(subject || subjectFactory, ?selector)``
- ``connect()``
- ``refCount()``
- ``publish()``
- ``publishBehavior(seed)``
- ``publishReplay(?bufferSize, ?windowSize)``
- ``publishLast()``
- ``share()``
