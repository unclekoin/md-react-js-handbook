[&#8678; go back to the table of contents](../../README.md)
# Change State / button / onClick
```js
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './app';

ReactDOM.render(<App />, document.getElementById('root'));
```
```js
// app.js
import React, { Component } from 'react';

class App extends Component {
  constructor(props) {
    super(props);

    this.state = {
      clicks: 0,
    };
  }

  componentDidMount() {
    if (this._unmounted) return;
    this.setState({ data });
  }

  componentWillUnmount() {
    this._unmounted = true;
  }

  render() {
    return (
      <div className="app">
        <h1>React App</h1>
        <div>Clicks: { this.state.clicks }</div>
        <button 
        onClick={ () => {
          this.setState({ clicks: this.state.clicks + 1 });
        } }>
        Click!
        </button>
      </div>
    );
  }
}

export default App;
```