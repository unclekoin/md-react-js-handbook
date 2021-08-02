[&#8678; go back to the table of contents](../README.md)
# Filter Data / input / onChange

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
// app.js
import React, { Component } from 'react';
import DataList from './data-list';

const data = [
  'lorem',
  'ipsum',
  'dolor',
  'sit',
  'amet',
  'consectetur',
  'adipisicing',
  'elit',
  'accusantium',
  'aliquid',
  'consequuntur',
  'delectus',
  'dignissimos',
  'expedita',
  'facere',
  'hic',
  'ipsam',
  'labore',
  'laboriosam',
  'maiores',
  'minus',
  'quidem',
  'quod',
  'voluptas',
  'Iste',
  'obcaecati',
  'perferendis',
  'quam',
  'quos',
  'tempore'
];

class App extends Component {
  constructor(props) {
    super(props);

    this.state = {
      data: ['test'],
      filteredData: []
    };

    this.onInputChange = this.onInputChange.bind(this);
  }

  componentDidMount() {
    if (this._unmounted) return;
    this.setState({ data, filtered: data });
  }

  componentWillUnmount() {
    this._unmounted = true;
  }

  onInputChange({ target: { value } }) {
    this.setState({
      filteredData: data.filter((item) => item.startsWith(value))
    });
  }

  render() {
    return (
      <div className="app">
        <h1>React App</h1>
        <input onChange={ this.onInputChange } type="text"/>
        <DataList data={ this.state.filteredData }/>
      </div>
    );
  }
}

export default App;
```