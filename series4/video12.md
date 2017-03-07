# Use groupBy in real RxJS applications
[Video](https://egghead.io/lessons/rxjs-use-groupby-in-real-rxjs-applications)

**groupBy** is very useful when we have many different data sources coming through the same observable (e.g. touch effects) and we want to split the data, apply some transformation based on the type of data, and then merge the stream back after the transformation.

```js
const bus$ = Rx.Observable.of(
  { code: 'en-us', value: '-TEST-' },
  { code: 'en-us', value: 'hello' },
  { code: 'es', value: '-TEST-' },
  { code: 'en-us', value: 'amazing' },
  { code: 'pt-br', value: '-TEST-' },
  { code: 'pt-br', value: 'olá' },
  { code: 'es', value: 'hola' },
  { code: 'es', value: 'mundo' },
  { code: 'en-us', value: 'world' },
  { code: 'pt-br', value: 'mundo' },
  { code: 'es', value: 'asombroso' },
  { code: 'pt-br', value: 'maravilhoso' },
).concatMap(x => Rx.Observable.of(x).delay(500))

// static partitioning, must know which languages appear
const lang$ = code => bus$
  .filter(obj => obj.code === code)
  .skip(1) // skip -TEST- value
  .map(obj => obj.value)

const enUS$ = lang$('en-us')
const es$ = lang$('es')
const ptBR$ = lang$('pt-br')

const all$ = Rx.Observable.merge(enUS$, es$, ptBR$)
all$.subscribe(console.log)
// hello amazing olá hola mundo world mundo asombroso maravilhoso

// dynamic partitioning
const dynmicAll$ = bus$
  .groupBy(obj => obj.code) // branch with inner observables
  .mergeMap(inner$ => inner$.skip(1).map(obj => obj.value))

dynmicAll$.subscribe(console.log)
// hello amazing olá hola mundo world mundo asombroso maravilhoso
```
