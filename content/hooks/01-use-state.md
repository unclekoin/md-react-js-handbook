[&#8678; go back to the table of contents](../../README.md)
# useState
```js
import React, { useState } from 'react';
import ReactDOM from 'react-dom';

const App = () => {
  return (
    <div>
      <HooksSwitcher />
    </div>
  )
}

const HooksSwitcher = () => {
  const [color, setColor] = useState('white');
  const [fontSize, setFontSize] = useState(14);

  return (
    <div style={{
      padding: 10,
      backgroundColor: color,
      border: '1px solid black',
      fontSize: fontSize
    }}>
      <p>Hello World</p>
      <button onClick={() => setColor('grey')}>
        Dark
      </button>
      <button onClick={() => setColor('white')}>
        Light
      </button>
      <button onClick={() => setFontSize(prev => prev + 1)}>
        +
      </button>
      <button onClick={() => setFontSize(prev => prev - 1)}>
        -
      </button>
    </div>
  )
}

ReactDOM.render( <App />, document.getElementById('root'));
```
```js
const Person = () => {
  const [firstName, setFirstName] = useState('Bob');
  const [lastName, setLastName] = useState('Smith');
  
  serFirstName('Mike');
}

const Person = () => {
  const [person, setPerson] = useState({
    firstName: 'Bob',
    lastName: 'Smith'
  });

  serPerson((person) => {
    return {...person, firstName: 'Mike'}
  });
}
```