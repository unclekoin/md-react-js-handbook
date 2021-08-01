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

  // Similar to  componentDidUpdate()
  useEffect(() => {
    console.log('useEffect');
  });

  // Similar to componentDidMount()
  useEffect(() => {
    console.log('useEffect');
  }, []);

  // Monitor changes in value
  useEffect(() => {
    console.log('useEffect');
  }, [value]);

  // Cleanup useEffect() 
  // Similar to componentWillUnmount()
  useEffect(() => {
    console.log('useEffect');
    return () => console.log('cleanup');
  }, [value])

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
### Example
```js
import React, {useEffect, useState} from "react";
import ReactDOM from "react-dom";

const App = () => {
  const [visible, setVisible] = useState(true);

  if (visible) {
    return (
      <div>
        <button onClick={() => setVisible(false)}>hide</button>
        <Notification/>
      </div>
    )
  } else {
    return <button onClick={() => setVisible(true)}>show</button>
  }
}

const Notification = () => {
  const [visible, setVisible] = useState(true);

  useEffect(() => {
    const timeout = setInterval(() => setVisible(false), 3000);
    return () => clearTimeout(timeout);
  }, [])
  
  return (
    <div>
      { visible && <p>Hello World!</p> }
    </div>
  )
}

ReactDOM.render(<App/>, document.getElementById("root"));
```
### Example. Avoiding Race Conditions when Fetching Data with React Hooks
```js
import React, { useEffect, useState } from "react";
import ReactDOM from "react-dom";

const App = () => {
  const [value, setValue] = useState(1);

  return (
    <div>
      <button onClick={ () => setValue((v) => v < 10 ? v + 1 : 1) }>
        +
      </button>
      <UserInfo id={ value }/>
    </div>
  )
}

const UserInfo = ({ id }) => {

  const [name, setName] = useState(null);

  useEffect(() => {
    let cancelled = false;
    fetch(`https://jsonplaceholder.typicode.com/users/${ id }`)
      .then(res => res.json())
      .then(data => !cancelled && setName(data.name))
      .catch(error => console.log(error));
    return () => cancelled = true;
  }, [id]);

  return (
    <div>{ id } - { name }</div>
  )
}

ReactDOM.render(<App/>, document.getElementById("root"));

```