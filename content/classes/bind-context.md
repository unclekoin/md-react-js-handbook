[&#8678; go back to the table of contents](../../README.md)
# Context Binding for Instance of Class

## Example 1.
```js
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import './index.css';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 0
    };

    this.counterHandler = this.counterHandler.bind(this);
  }

  counterHandler()  {
    this.setState((state) => ({
      counter: ++state.counter
    }));
  };

  render() {
    const { number } = this.props;
    const { counter } = this.state;

    return (
      <div>
        <h3>Counter #{ number }: { counter }</h3>
        <button onClick={ this.counterHandler }>+</button>
      </div>
    );
  }
}

const Counters = () => {
  return (
    <div>
      <Counter number="1"/>
      <Counter number="2"/>
      <Counter number="3"/>
    </div>
  );
};

ReactDOM.render(<Counters/>, document.getElementById('root'));
```

## Example 2.
```js
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import './index.css';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 0
    };

    this.counterHandler = () => {
      this.setState((state) => ({
        counter: ++state.counter
      }))
    }
  }

  render() {
    const { number } = this.props;
    const { counter } = this.state;

    return (
      <div>
        <h3>Counter #{ number }: { counter }</h3>
        <button onClick={ this.counterHandler }>+</button>
      </div>
    );
  }
}

const Counters = () => {
  return (
    <div>
      <Counter number="1"/>
      <Counter number="2"/>
      <Counter number="3"/>
    </div>
  );
};

ReactDOM.render(<Counters/>, document.getElementById('root'));
```

## Example 3.
```js
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import './index.css';

class Counter extends Component {

  state = {
    counter: 0
  };

  counterHandler = () => {
    this.setState((state) => ({
      counter: ++state.counter
    }))
  }

  render() {
    const { number } = this.props;
    const { counter } = this.state;

    return (
      <div>
        <h3>Counter #{ number }: { counter }</h3>
        <button onClick={ this.counterHandler }>+</button>
      </div>
    );
  }
}

const Counters = () => {
  return (
    <div>
      <Counter number="1"/>
      <Counter number="2"/>
      <Counter number="3"/>
    </div>
  );
};

ReactDOM.render(<Counters/>, document.getElementById('root'));
```