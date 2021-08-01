[&#8678; go back to the table of contents](../../README.md)
# useCallback

```js
import React, { useEffect, useState, useCallback } from "react";
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

// get data
const getUser = (id) => {
  return fetch(`https://jsonplaceholder.typicode.com/users/${ id }`)
    .then(res => res.json())
    .then(data => data);
}

// get data from async function
const useRequest = (request) => {
  const [dataState, setDataState] = useState(null);

  useEffect(() => {
    let cancelled = false;
    request()
      .then(data => !cancelled && setDataState(data))
    return () => cancelled = true;
  }, [request]);

  return dataState;
}

// useCallback()
const useUserInfo = (id) => {
  const request = useCallback(() => getUser(id), [id])
  return useRequest(request);
}

const UserInfo = ({ id }) => {
  const data = useUserInfo(id);

  return (
    <div>{ id } - { data && data.name }</div>
  )
}

ReactDOM.render(<App/>, document.getElementById("root"));
```