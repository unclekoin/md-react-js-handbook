[&#8678; go back to the table of contents](../../README.md)
# useEffect
```js
import React, {useEffect, useState, Component} from "react";
import ReactDOM from "react-dom";

const App = () => {
  const [value, setValue] = useState(0);
  const [visible, setVisible] = useState(true);

  if (visible) {
    return (
      <div>
        <button onClick={() => setValue(v => v + 1)}>+</button>
        <button onClick={() => setVisible(false)}>hide</button>
        <HookCounter value={value} />
        <ClassCounter value={value}/>
      </div>
    )
  } else {
    return <button onClick={() => setVisible(true)}>show</button>
  }
}

const HookCounter = ({ value }) => {
```
*Analog of componentDidUpdate()*
```js
  useEffect(() => {
    console.log('useEffect');
  });
```
*Analog of componentDidMount()*
```js
  useEffect(() => {
    console.log('useEffect');
  }, []);
```
*Monitor changes in value*
```js
  useEffect(() => {
    console.log('useEffect');
  }, [value]);
```
*cleanup useEffect()*
```js
  useEffect(() => {
    console.log('useEffect');
    return () => console.log('cleanup');
  }, [value])
```
```js
  return <div>{ value }</div>
}

class ClassCounter extends Component {
  componentDidMount() {
    console.log('class: mount');
  }

  componentDidUpdate() {
    console.log('class: update');
  }

  componentWillUnmount(props) {
    console.log('class: unmount');
  }

  render() {
    return <div>{this.props.value}</div>
  }
}

ReactDOM.render(<App/>, document.getElementById("root"));
```