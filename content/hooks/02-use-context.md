[&#8678; go back to the table of contents](../../README.md)
# useContext
```js
import React, {useContext} from "react";
import ReactDOM from "react-dom";

const ContextA = React.createContext();
const ContextB = React.createContext();

const App = () => {

  return (
    <ContextB.Provider value="1">
      <ContextA.Provider value="Hello World">
        <A/>
        <B/>
      </ContextA.Provider>
    </ContextB.Provider>
  )
}

const A = () => {
  const value = useContext(ContextA);

  return <p>{value}</p>
}

const B = () => {
  const value = useContext(ContextB);

  return <p>{value}</p>
}

ReactDOM.render(<App/>, document.getElementById("root"));
```