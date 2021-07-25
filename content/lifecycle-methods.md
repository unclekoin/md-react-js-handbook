[&#8678; go back to the table of contents](../README.md)
# Commonly Used Lifecycle Methods
<img src="../assets/images/lifecycle.jpeg">

```js
render() {
  return (
    <div>
      ...
    </div>
  )
}

constructor(props) {
  super(props)
}

componentDidMount()

componentDidUpdate(prevProps, prevState, snapshot)

componentWillUnmount()

shouldComponentUpdate(nextProps, nextState)

static getDerivedStateFromProps(props, state)

getSnapshotBeforeUpdate(prevProps, prevState)

static getDerivedStateFromError(error)

componentDidCatch(error, info)
