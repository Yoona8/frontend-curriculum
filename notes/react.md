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
import React { Component } from 'react';
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

const player = () => {
  return (
    <h2>I'm {}! My level is {}</h2>
  );
};

export default user;
```
```JavaScript
// App.js
import React { Component } from 'react';
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