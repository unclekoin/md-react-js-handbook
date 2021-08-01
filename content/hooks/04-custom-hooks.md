[&#8678; go back to the table of contents](../../README.md)
# Custom Hooks

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

const useUserInfo = (id) => {
  const [name, setName] = useState(null);

  useEffect(() => {
    let cancelled = false;
    fetch(`https://jsonplaceholder.typicode.com/users/${ id }`)
      .then(res => res.json())
      .then(data => !cancelled && setName(data.name))
      .catch(error => console.log(error));
    return () => cancelled = true;
  }, [id]);

  return name;
}

const UserInfo = ({ id }) => {
  const name = useUserInfo(id);

  return (
    <div>{ id } - { name }</div>
  )
}

ReactDOM.render(<App/>, document.getElementById("root"));
```