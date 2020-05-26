# Frontend Curriculum

## HTML CSS

<details>
<summary>HTML basic structure</summary>

```HTML
<!doctype html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <!-- optional: start -->
  <meta name="keywords" content="...">
  <meta name="description" content="...">
  <!-- optional: end -->
  <title>Title</title>
  <link href="#" rel="stylesheet">
</head>
<body>
</body>
```

</details>

<details>
<summary>Text HTML and CSS</summary>

```HTML
<ol start/reversed> <!-- bool for changing the order -->
<q cite="https://..."> <!-- cite the address -->
<ins/del/time datetime="ISO string format">Today</ins/del/time> <!-- ISO for computers, text for humans -->
```

</details>

Embedded content tags
Tables in HTML and CSS
Forms
Selectors
Block model
Floats
Flexbox
Grid
Positioning
Backgrounds
Borders and outlines
Shadows
Gradients
Transformations
Transitions
Animations

## JavaScript

ECMAScript
Constants and variables
Data structures
Numbers
Strings
Iterables
Objects
Constructors and prototypes
Classes
Operators
Functions
Control structures
Modules
DOM
Events

<details>
<summary>Async JavaScript (promises and callbacks, async/await)</summary>

  <details>
  <summary>Sync data loading</summary>

  ```JavaScript
  const getResponse = (url) => {
    const xhr = new XMLHttpRequest();
    xhr.open('GET', url, false);
    xhr.send();
    // we can do it like that, because it's a sync request
    // return will happen after we get the response
    return xhr.response;
  };
  const data = getResponse('https://data.com/users');
  ```

  </details>
  
  Async ES5 (callbacks)
  Async ES6 (promises) 

</details>

Http requests
Browser storage
Meta-programming
Performance and optimizations
Security
Deploying
Testing
Debugging
Browser support
Tools and workflow
Libraries
Frameworks

## OOP

Inheritance and polymorphism
Data-binding

## Procedural programming

## Functional programming

## Data structures and Algorithms

## TypeScript

## Angular

## React

## Canvas API

## WebGL and animations

## Graphics

SVG

## Serverless

## Firebase

## Web components

## Chrome Dev Tools

<details>
<summary>Shortcuts and tips</summary>

- Shortcuts (menu => shortcuts)
  - `ctrl + F` search (by any word)
  - `ctrl + shift + F` search across all sources
  - `tab` `tab + shift` step forward / back when adding changes
  - `H` hide chosen element of the html (adds `visibility: hidden;`)
  - `F2` to be able to edit html
- `document.body.contentEditable = true;`

</details>

## Webpack
