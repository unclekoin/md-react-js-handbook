[&#8678; go back to the table of contents](../../README.md)
# Filter Data / input / onChange / Hooks
```js
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './app';

ReactDOM.render(<App />, document.getElementById('root'));
```
```js
// data-list.js
import React from 'react';

export default function DataList({ data = [] }) {
  return (
    <ul>
      {
        data.map((item, index) => <li key={ index }>{ item }</li>)
      }
    </ul>
  )
}
```
```js
// service.js
const data = ['abdomen',
  'accordion',
  'ace',
  'acorn',
  'active',
  'acute angle',
  'aerosol',
  'aileron',
  'aircraft',
  'alarm clock',
  'albatross',
  'album',
  'alligator',
  'almond',
  'alternate angles',
  'ammonite',
  'amphibian',
  'amphitheater',
  'amplifier',
  'amplitude',
  'anchor',
  'angle',
  'ankh',
  'ankle',
  'ant',
  'antelope',
  'antenna',
  'anther']

export default async function  fetchData () {
  return await data;
}
```
```js
// app.js
import React, { useState, useEffect } from 'react';
import './app.css';
import DataList from './data-list';
import fetchData from './service';

const App = () => {
  const [data, setData] = useState([]);
  const [inputValue, setInputValue] = useState('');

  useEffect(() => {
    fetchData().then(setData);
  }, []);

  return (
    <div className="app">
      <input onChange={(e) => setInputValue(e.target.value)} type="text"/>
      { inputValue && <DataList data={ data.filter((item) => item.startsWith(inputValue)) }/> }
    </div>
  );
};

export default App;
```