# Using a Subject as an Event Bus

[Video](https://egghead.io/lessons/rxjs-using-a-subject-as-an-event-bus)

We can use the **observer** methods of the **subject** (``next``, ``error``, and ``complete``) to manually control the **observers**. When manually controlling observables, we must be careful not to violate the observable contract (i.e. sending more than one of error and complete events).

####

```js
const subject = new Rx.Subject()

const observerA = {
  next: x => console.log(`A next ${x}`),
  error: err => console.log(`A error ${err}`),
  complete: () => console.log('A done'),
}

subject.subscribe(observerA)

const observerB = {
  next: x => console.log(`B next ${x}`),
  error: err => console.log(`B error ${err}`),
  complete: () => console.log('B done'),
}

setTimeout(() => subject.subscribe(observerB), 2000)

// manually control the observers
subject.next(1)
subject.next(2)
subject.next(3)

setInterval(() => subject.next(10), 1000)
```

##### A React example
```js
class Hello extends React.Component {
  constructor() {
    super()
    this.state = {count: 0}
    this.subject = new Rx.Subject()

    // our event bus
    this.subject
      .map(ev => +1)
      .scan((acc, x) => acc + x)
      .delay(1000)
      .subsribe(count => this.setState({count}))
  }

  render() {
    return (
      <div onClick={ev => this.subject.next(ev)}>
        {`${this.state.count} Hello ${this.props.name}`}
      </div>
    )
  }
}

ReactDOM.render(<Hello name='World'/>, document.querySelector('#app'))
```
