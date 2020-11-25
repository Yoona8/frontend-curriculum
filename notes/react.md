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
- `shouldComponentUpdate` is used to prevent the `render()` calls, but not every `render()` call updates the DOM
  - `render()` is called
  - React stores 2 versions of Virtual DOM (old and re-rendered) - working with virtual DOM is faster than light DOM
  - React compares 2 versions of Virtual DOM
  - if there are any differences - React updates only the affected parts

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
  - access to state (via hooks)
  - **NO** lifecycle hooks
- class-based components (containers, smart, stateful)
  - access to state
  - lifecycle hooks

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
<summary>How to return JSX not wrapped in one container? (Rendering adjacent JSX)</summary>

```JavaScript
// return an array of elements
return [
  // add unique keys (like we work with loop to create JSX)
  <p key="p1">Some test here!</p>,
  <section key="s2">
    <h2>Some section title</h2>
  </section>,
  <ul key="u3">
    <li>Some item</li>
    <li>One more item</li>
  </ul>
];

// use a higher order component
const Aux = props => props.children;
return (
  <Aux>
    <p>Some test here!</p>
    <section>
      <h2>Some section title</h2>
    </section>
    <ul>
      <li>Some item</li>
      <li>One more item</li>
    </ul>
  </Aux>
);

// or use React Fragment (works like Aux component)
return (
  <React.Fragment>
    <p>Some test here!</p>
    <section>
      <h2>Some section title</h2>
    </section>
    <ul>
      <li>Some item</li>
      <li>One more item</li>
    </ul>
  <React.Fragment>
);
```

</details>

<details>
<summary>What is a higher order component?</summary>

- wrapper for another component (like Aux component)
- wrapper with specific class names for another component
```JavaScript
import React from 'react';

// creating a component
const ClassWrapper = props => (
  <div className={props.classes}>{props.children}</div>
);

// or using a function to create a component
const wrapWithClass = (InnerComponent, className) => {
  return props => (
    <div class={className}>
      <InnerComponent />
    </div>
  );
};

// usage with function, here classes are CSS modules classes
export default wrapWithClass(InnerComponent, classes.InnerComponent);

export default ClassWrapper;
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
<summary>How to pass the unknown props? (Like when using a HOC)</summary>

```JavaScript
import React from 'react';

const wrapWithClass = (InnerComponent, className) => {
  // {...props} will convert all the props into attributes
  return props => (
    <div class={className}>
      <InnerComponent {...props} />
    </div>
  );
};
```

</details>

<details>
<summary>How to use PropTypes</summary>

- first you have to install the prop-types package in dependencies
```JavaScript
import PropTypes from 'prop-types';

class User extends Component {
  render() {
    // ...
  }
}

User.propTypes = {
  click: PropTypes.func,
  name: PropTypes.string,
  level: PropTypes.number
  // advanced types are also allowed
};
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
<summary>How to update the state correctly based on the previous state?</summary>

- React doesn't update the state immediately, runs in an async way
- the issue is that the previous state might be different to what we expect
```JavaScript
// wrong way
this.setState({
  users: users,
  changeCounter: this.state.changeCounter + 1
});

// proper way
this.setState((prevState, props) => ({
  users: users,
  changeCounter: prevState.changeCounter + 1
}));
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
<summary>What are Refs and how to use them?</summary>

- can be used with class-based components or with React Hooks
- used to access the element in your component

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
<summary>What is a component lifecycle?</summary>

- only available in class-based component
- the order
```JavaScript
// Creation Lifecycle
// 0 - set up state
// don't add any side-effects (poor performance and re-render)
// can also initiate state here instead of using a field
constructor(props) {...}
// 1 - sync state when props change (rare usage)
// don't add any side-effects (poor performance and re-render)
static getDerivedStateFromProps(props, state) {
  return state;
}
// 3 - prepare and structure the JSX code
render() {}
// 3.5 deprecated - before the componentDidMount
componentWillMount() {}
// 4 - runs after all the child components are created
// here you can cause side effects
// but don't update the state (triggers re-render)
componentDidMount() {}
```
```JavaScript
// Update Lifecycle
// 1
static getDerivedStateFromProps(props, state) {
  return state;
}
// 1.5 deprecated
componentWillReceiveProps(props) {}
// 2
shouldComponentUpdate(nextProps, nextState) {
  return true || false;
}
// 3
getSnapshotBeforeUpdate(prevProps, prevState) {
  return 'some value' || null;
}
// 4 - prepare and structure the JSX code
render() {}
// 4.5 deprecated
componentWillUpdate() {}
// 5 - runs after all the child components are created
componentDidUpdate(prevProps, prevState, snapshot) {
  // returned from getSnapshotBeforeUpdate
  console.log(snapshot);
}
```
```JavaScript
// Cleanup Lifecycle
// 1
componentWillUnmount() {
  // run the code right before the component is removed
}
```

</details>

<details>
<summary>How to manage lifecycle (partially) with hooks?</summary>

- for functional components (a combination of `componentDidMount` and `componentDidUpdate`)
- executes for every render cycle (not render to DOM, but to ReactDOM)
```JavaScript
// no parameters
useEffect(() => {
  // http request...
});

// to execute only on some property changes
// can use many useEffect calls for different props
useEffect(() => {
  // http request...
}, [props.users]);

// to execute only when the component renders the first time
// have to pass [] (like no dependencies = never changes = never triggered)
useEffect(() => {
  // http request...
}, []);

// to do the cleanup every update
useEffect(() => {
  // ...
  return () => {
    // cleanup here
    // this function runs before the main useEffect function
    // but after the first render cycle
  };
});

// to do the cleanup when the component is destroyed
useEffect(() => {
  // ...
  return () => {};
}, []);
```

</details>

<details>
<summary>How and when to optimise the component?</summary>

- optimise when you really need it
  - if the parent updates, but the child doesn't in most cases
- otherwise you'll be running extra logic
```JavaScript
// class-based
shouldComponentUpdate(nextProps, nextState) {
  return nextProps.users !== this.props.users;
}
// if you want to check all the props, extend from PureComponent
class App extends PureComponent {}

// function-based
export default React.memo(User);
```

</details>

<details>
<summary>Learn more</summary>

- [Supported events](https://reactjs.org/docs/events.html#supported-events)
- [Introducing JSX](https://reactjs.org/docs/introducing-jsx.html)
- [Rendering Elements](https://reactjs.org/docs/rendering-elements.html)
- [Components and Props](https://reactjs.org/docs/components-and-props.html)
- [SyntheticEvent](https://reactjs.org/docs/events.html)
- [Using the Effect Hook](https://reactjs.org/docs/hooks-effect.html)
- [State and Lifecycle](https://reactjs.org/docs/state-and-lifecycle.html)
- [Typechecking With PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html)
- [Higher-Order Components](https://reactjs.org/docs/higher-order-components.html)
- [Refs and the DOM](https://reactjs.org/docs/refs-and-the-dom.html)

</details>

## Context API
<details>
<summary>How to use the Context API and why?</summary>

- in cases when you need to chain props (pass through one component to its children)
- stored in a different folder (context)

</details>

## Lists and Conditions
<details>
<summary>How to render the content conditionally?</summary>
</details>

<details>
<summary>How to render lists based on some data?</summary>
</details>

<details>
<summary>What is `key` property and why should we use it?</summary>

- always should be on the wrapping element

</details>

<details>
<summary>Learn more</summary>

- [Conditional Rendering](https://reactjs.org/docs/conditional-rendering.html)
- [Lists and Keys](https://reactjs.org/docs/lists-and-keys.html)

</details>

## Styling
<details>
<summary>How to style components?</summary>

- in the separate file, but styles are going to be global
- inline styles with style object applied to the component (but can't use media, pseudo- classes and elements)
```JavaScript
// ...
render() {
  const style = {
    backgroundColor: 'green'
  };

  return (
    <div>
      <p style={style}>Some text here</p>
    </div>
  );
}
// ...
```

</details>

<details>
<summary>How to change styles dynamically with inline approach?</summary>
</details>

<details>
<summary>How to set class names dynamically?</summary>
</details>

<details>
<summary>How and why do we use Radium?</summary>
</details>

<details>
<summary>How and why do we use Styled Components?</summary>
</details>

<details>
<summary>How to enable and work with CSS Modules?</summary>
</details>

<details>
<summary>Learn more</summary>

- [CSS Modules](https://github.com/css-modules/css-modules)
- [How to Use CSS Modules with Create React App](https://medium.com/nulogy/how-to-use-css-modules-with-create-react-app-9e44bec2b5c2)
- [Adding a CSS Modules Stylesheet](https://create-react-app.dev/docs/adding-a-css-modules-stylesheet/)

</details>

## Error Handling
<details>
<summary>What is Error Boundary?</summary>

- a component with method `componentDidCatch`
- won't work in the development mode

</details>

<details>
<summary>Learn more</summary>

- [Error Boundaries](https://reactjs.org/docs/error-boundaries.html)

</details>

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