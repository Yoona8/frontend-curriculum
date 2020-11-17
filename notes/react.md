# React
## Overall
<details>
<summary>Why should you choose React?</summary>

- if you want to learn faster (choose React or Vue instead of Angular)
- if your project is going to develop gradually in many steps, extending the functionality (choose React or Vue due to the best compatibility)
- when state becomes difficult to handle with vanilla JavaScript
- focus on logic and not on preventing your application from exploding
- huge ecosystem, community, high performance, development
- easy to use with multi page applications for widgets
- works with a copy of DOM (compares to the actual DOM, renders only the changed parts, less traffic used, good for mobile device)

</details>

<details>
<summary>What are the core concepts of React?</summary>

- `props` and `state` are the core concepts

</details>

<details>
<summary>How and when does React update the DOM?</summary>

- only changes in `props` or `state` trigger React to re-render components and update the DOM in the browser

</details>

<details>
<summary>Learn more</summary>

- [React official](https://reactjs.org/)
- [Create React App official](https://create-react-app.dev/)
- [ ] [Learn React](https://academind.com/learn/react/)

</details>

## Setup
<details>
<summary>How to install React with Create React App?</summary>

- look for current installation on official website
- `react` for working with React
- `react-dom` for rendering into the DOM
- `react-scripts` all the new workflow, ES6+ features support, etc.

</details>

<details>
<summary>What is the basic file structure?</summary>

```bash
app-name
| public
|-| index.html # where the app will be injected (contains root element)
| src
|-| index.js # starting point, renders the app to the DOM
```

</details>

## Components
<details>
<summary>What are the ways to create a component?</summary>

- functional components (presentational, dumb, stateless) - best practice
- class-based components (containers, smart, stateful)

</details>

<details>
<summary>What is JSX?</summary>

- React uses JSX to create elements (compiled to normal JS code)
- JSX is not HTML, even the tags are converted into HTML by React
- basic component is a function, which returns some JSX
- component has to be wrapped in one HTML element

</details>

<details>
<summary>How to create a simple component and render it?</summary>

```JavaScript
// have to import to convert JSX into React.createElement
import React from 'react';

// props contain all the attributes given in render
function User(props) {
  // should return the html to render
  return (
    <div className="user">
      <h2>{props.name}</h2>
    </div>
  );

  // when rendered, JSX actually looks like this
  return React.createElement('div', {
    className: 'user'
  }, React.createElement('h2', null, 'Some text'));
}

// allows to render JS function as a component into a DOM
ReactDOM.render(<User name="Emma" />, document.querySelector('#user-1'));
ReactDOM.render(<User name="Hannah" />, document.querySelector('#user-2'));

// better to render only once
const app = (
  <div>
    <User name="Emma" />
    <User name="Hannah" />
  </div>
);

ReactDOM.render(app, document.querySelector('#root'));
```

</details>

<details>
<summary>How to import and use a component?</summary>

```JavaScript
// ./User/User.js
import React from 'react';

const user = () => {
  return (
    <h2>I'm Maya!</h2>
  );
};

export default user;
```
```JavaScript
// App.js
import React, { Component } from 'react';
// have to use an uppercase
// (to be identified by React as a custom component)
// all the lowercase are reserved for HTML syntax
import User from './User/User';

class App extends Component {
  render() {
    return (
      <div className="container">
        <User />
        <User></User>
      </div>
    );
  }
}
```

</details>

<details>
<summary>How to output dynamic content?</summary>

```JavaScript
// ./Player/Player.js
import React from 'react';

const player = () => {
  // inside {} no multiline code allowed
  return (
    <h2>I'm Harry! I'm level {Math.random()}</h2>
  );
};

export default player;
```

</details>

<details>
<summary>How to work with props and children?</summary>

```JavaScript
// ./Player/Player.js
import React from 'react';

// props holds all the properties passed as attributes from parent
const player = (props) => {
  return (
    <h2>I'm {props.name}! My level is {props.level}</h2>
    // to access the content provided inside the component tag
    <p>{props.children}</p>
  );
};

export default player;
```
- if created as a class - accessible via `this.props`
```JavaScript
// ./Player/Player.js
import React from 'react';

// props holds all the properties passed as attributes from parent
class Player extends Component {
  render() {
    return (
      <h2>I'm {this.props.name}! My level is {this.props.level}</h2>
    );
  }
};

export default Player;
```
```JavaScript
// App.js
import React, { Component } from 'react';
import Player from './Player/Player';

class App extends Component {
  render() {
    return (
      <div className="container">
        <Player name="Harry" level="10" />
        <Player name="Ron" level="10">My house is Griffindor!</Player>
      </div>
    );
  }
}
```

</details>

<details>
<summary>What is a component state and how to use it?</summary>

- if the state changes, React updates the DOM
- only the affected parts are re-rendered
- could be used only in class components
```JavaScript
// App.js
import React, { Component } from 'react';
import Player from './Player/Player';

class App extends Component {
  // can define a state property only for classes
  // which extended from the Component
  // managed from the inside of the component
  state = {
    players: [
      { name: 'Harry', level: 10 },
      { name: 'Ron', level: 10 }
    ]
  }

  render() {
    return (
      <div className="container">
        <Player 
          name={this.state.players[0].name}
          level={this.state.players[0].level} />
        <Player
          name={this.state.players[1].name}
          level={this.state.players[1].level}
        >My house is Griffindor!</Player>
      </div>
    );
  }
}
```

</details>

<details>
<summary>How to handle events in a component?</summary>

```JavaScript
// App.js
import React, { Component } from 'react';
import Player from './Player/Player';

class App extends Component {
  state = {
    players: [
      { name: 'Harry', level: 10 },
      { name: 'Ron', level: 10 }
    ]
  }

  onButtonClick = () => {
    console.log(this);
  };

  render() {
    return (
      <div className="container">
        <button onClick={this.onButtonClick} type="button">
          Change player
        </button>
        <Player 
          name={this.state.players[0].name}
          level={this.state.players[0].level} />
        <Player
          name={this.state.players[1].name}
          level={this.state.players[1].level}
        >My house is Griffindor!</Player>
      </div>
    );
  }
}
```

</details>

<details>
<summary>How to work with the state inside the component?</summary>

- React updates the parts of DOM when state or props change
```JavaScript
// App.js
import React, { Component } from 'react';
import Player from './Player/Player';

class App extends Component {
  state = {
    players: [],
    otherState: 'some state value'
  }

  onButtonClick = () => {
    // can't mutate the state like that
    this.state.players[0].name = 'Ron';
    // have to use a special method
    // inherited from the Component
    // merges with the existing state
    // the otherState stays the same
    this.setState({
      players: [
        { name: 'Ron', level: 10 }
        { name: 'Ron', level: 10 }
      ]
    });
  };

  render() {
    return (
      <div className="container">
        <button onClick={this.onButtonClick} type="button">
          Change player
        </button>
        <Player 
          name={this.state.players[0].name}
          level={this.state.players[0].level} />
        <Player
          name={this.state.players[1].name}
          level={this.state.players[1].level}
        >My house is Griffindor!</Player>
      </div>
    );
  }
}
```
- with hooks in the component function
```JavaScript
// App.js
import React, { useState } from 'react';
import Player from './Player/Player';

const App = props => {
  // returns an array with exactly 2 elements
  // (current state, function that allows to update the state)
  const [playersState, setPlayersState] = useState({
    players: [],
    // when we change the players state, will be removed
    otherState: 'some state value'
  });
  // set otherState here not to be rewritten
  const [otherState, setOtherState] = useState({
    otherState: 'some value'
  });
  // or any other value
  useState('some other value');

  const onButtonClick = () => {
    // rewrites the state, otherState will be lost
    setPlayersState({
      players: [
        { name: 'Ron', level: 10 }
        { name: 'Ron', level: 10 }
      ]
    });
  };

  return (
    <div className="container">
      <button onClick={onButtonClick} type="button">
        Change player
      </button>
      <Player 
        name={playersState.players[0].name}
        level={playersState.players[0].level} />
      <Player
        name={playersState.players[1].name}
        level={playersState.players[1].level}
      >My house is Griffindor!</Player>
    </div>
  );
}
```

</details>

<details>
<summary>How to pass method references between components?</summary>

- methods can be passed as props
```JavaScript
// ./Player/Player.js
import React from 'react';

const Player = (props) => {
  return (
    <h2 onClick={props.click}>
      I'm {props.name}! My level is {props.level}
    </h2>
    <p>{props.children}</p>
  );
};

export default Player;
```
```JavaScript
// App.js
import React, { Component } from 'react';
import Player from './Player/Player';

class App extends Component {
  state = {
    players: [
      { name: 'Harry', level: 10 },
      { name: 'Ron', level: 10 }
    ]
  }

  onButtonClick = () => {
    console.log(this);
  };

  // bind is more efficient if args needed
  render() {
    return (
      <div className="container">
        <button onClick={this.onButtonClick} type="button">
          Change player
        </button>
        <Player 
          name={this.state.players[0].name}
          level={this.state.players[0].level}
          click={this.onButtonClick}
          click={this.onButtonClick.bind(this, 'Harry')}
          click={() => this.onButtonClick('Harry')}
        />
        <Player
          name={this.state.players[1].name}
          level={this.state.players[1].level}
        >My house is Griffindor!</Player>
      </div>
    );
  }
}
```

</details>

<details>
<summary>How to implement a two-way binding?</summary>

```JavaScript
// ./Player/Player.js
import React from 'react';

const Player = (props) => {
  return (
    <h2 onClick={props.click}>
      I'm {props.name}! My level is {props.level}
    </h2>
    <input
      type="text"
      onChange={props.changed}
      value={props.name}
    />
    <p>{props.children}</p>
  );
};

export default Player;
```
```JavaScript
// App.js
import React, { Component } from 'react';
import Player from './Player/Player';

class App extends Component {
  state = {
    players: [
      { name: 'Harry', level: 10 },
      { name: 'Ron', level: 10 }
    ]
  }

  onButtonClick = () => {
    console.log(this);
  }

  onNameChanged = (evt) => {
    console.log(evt.target.value);
  } 

  render() {
    return (
      <div className="container">
        <button onClick={this.onButtonClick} type="button">
          Change player
        </button>
        <Player 
          changed={this.onNameChanged}
          name={this.state.players[0].name}
          level={this.state.players[0].level} />
        <Player
          name={this.state.players[1].name}
          level={this.state.players[1].level}
        >My house is Griffindor!</Player>
      </div>
    );
  }
}
```

</details>

<details>
<summary>Learn more</summary>

- [Supported events](https://reactjs.org/docs/events.html#supported-events)

</details>

## Styling

## HTTP Requests

## Routing

## Forms and validation

## Redux

## Authentication

## Animations

## SSR

## Debugging

## Testing

## Deployment