[&#8678; go back to the table of contents](../../README.md)
# useMemo

```js
import React, { useEffect, useState, useCallback, useMemo } from "react";
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
// useMemo()
  const initialState = useMemo(() => ({
    data: null,
      loading: true,
      error: null
  }), [])
  const [dataState, setDataState] = useState(initialState);

  useEffect(() => {
    setDataState(initialState)
    let cancelled = false;
    request()
      .then(data => !cancelled && setDataState({
        data,
        loading: false,
        error: null
      }))
      .catch((error) => !cancelled && setDataState({
        data: null,
        loading: false,
        error
      }))
    return () => cancelled = true;
  }, [request, initialState]);

  return dataState;
}

// useCallback()
const useUserInfo = (id) => {
  const request = useCallback(() => getUser(id), [id])
  return useRequest(request);
}

const UserInfo = ({ id }) => {
  const { data, loading, error } = useUserInfo(id);

  if (error) return <div>Something went wrong!</div>;
  if (loading) return <div>Loading...</div>;

  return (
    <div>{ id } - { data.name }</div>
  )
}

ReactDOM.render(<App/>, document.getElementById("root"));

```