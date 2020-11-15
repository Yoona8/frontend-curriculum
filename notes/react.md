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

- [ ] [Learn React](https://academind.com/learn/react/)

</details>

## Setup
<details>
<summary>How to install React?</summary>

- react.min.js for working with React
- react-dom.min.js for rendering into the DOM

</details>

## Components
<details>
<summary>How to create a simple component and render it?</summary>

- uses JSX (compiled to normal JS code)
- basic component is a function
- component has to be wrapped in one HTML element
```JavaScript
// props contain all the attributes given in render
function User(props) {
  // should return the html to render
  return (
    <div className="user">
      <h2>{props.name}</h2>
    </div>
  );
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

## Styling

## HTTP Requests

## Routing

## Forms and validation

## Redux

## Authentication

## Debugging