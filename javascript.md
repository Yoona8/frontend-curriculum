# JavaScript

- [To content](#readme.md)

- 3 Data types and structures
- 4 Numbers
- 5 Strings
- 6 Iterables
- 7 Objects
- 9 Constructors and prototypes
- 10 Classes
- 12 Control structures
- 13 Modules
- 14 DOM
- 17 Http requests
- 18 Browser storage
- 19 Meta-programming
- 20 Performance and optimizations
- 21 Security
- 22 Deploying
- 23 Testing
- 24 Debugging
- 25 Browser support
- 26 Tools and workflow
- 27 Libraries
- 28 Frameworks

## 1 - ECMAScript
<details>
<summary>Notes</summary>

Global changes:
- new strategy of spec updating
- problem concepts
  - hoisting
  - `var` rewriting
  - scope (var with no block-scope)
- new opportunities
  - `let`, `const` - hoisting, scope, rewriting solved
  - template strings
  - function default params
  - arrow functions
  - destructuring
- better objects

</details>

## 2 - Constants and variables
<details>
<summary>Examples</summary>

```JavaScript
// constants - code agreements
// protected values, hardcoded (default configs, physical consts, coefficients)
// distinguished by it's appearance
// any constant declares as a const
// is immutable
const Earth = {
  RADIUS: 6.371,
  GRAVITATION: 6.67408
};
const DEFAULT_NAMES = ['Michael', 'Anna', 'Chris'];
const LIGHT_SPEED = 255792458;

// consts
// not any const = constant
// declares a variable with immutable link
const element = document.querySelector('p');
const arr = [1, 2, 3, 4];
```

</details>

## 8 - Functions
<details>
<summary>Notes</summary>

- function without `return` statement returns `undefined`

```JavaScript
// default params
// Earlier
var doSomething = function (caption, amount, isChecked) {
  if (typeof isChecked === 'undefined') {
    isChecked = false;
  }
};

// ES2015
const doSomething = (caption, amount, isChecked = false) => {
  // some code here
};
```

- doesn't have it's own scope (only lexical) - when global, `this === window`
- doesn't have `arguments` object
- can't rewrite `this` (`bind` and `call` won't work)
  - can't be used as a constructor, no `new` keyword
  - can't be method of an object or prototype

```JavaScript
// arrow functions
// only 1 param?
const doSomething = param => console.log(param);

// only 1 line?
// = return left * right;
const doSomething = (left, right) => left * right;

// return object?
const getWizard = (name, level) => ({
  name,
  level
});
```

</details>

## 11 - Expressions and Operators
<details>
<summary>Destructuring: Arrays and alike</summary>

- for iterable structures only (doesn't work on strings!)
- all the elements go in an order, can't address the last one

```JavaScript
const numbers = [1, 2, 3, 4, 5];
// before 
const first = numbers[0];
const third = numbers[2];
// with destructuring
const [first, , third] = numbers;
// when there is no value, can use defaults
const [first, , , , , sixth = 45] = numbers;
// good for swapping the values
let first = 'Harry';
let second = 'Ron';
[first, second] = [second, first];
// can destruct the function result
const [first, , third] = getNumbers();
// or function parameters
const printValues = ([first = 4, , third = 7]) => {
  console.log(`${first} ${third}`);
};
printValues(document.querySelectorAll('li'));
printValues([1, 2]);
printValues([]);
printValues(); // error: undefined is not iterable
```

</details>

<details>
<summary>Destructuring: Objects</summary>

```JavaScript
const cat = {
  name: 'Mini',
  location: 'London',
  color: 'Auburn',
  address: {
    street: 'Some street'
  },
  'home city': 'London'
};
// propOfAnObject: varName = default
const {name: catName, color: catColor = 'White'} = cat;
// with folded objects
const {address: {street: catStreet}} = cat;
// for combined prop use quotes
const {'home city': catCity} = cat;

// great to use for DOM nodes
const elements = document.querySelectorAll('li');
for (let i = 0; i < elements.length; i++) {
  const {textContent: text} = elements[i];
  console.log(text);
}

// can combine [] and {} destructuring
const [, {textContent: text}] = document.querySelectorAll('li');
```

</details>

## 15 - Events
<details>
<summary>Events</summary>

- difference between `change` and `input`
  - `change` works when `field.value` changed and the user finished to enter the value (moved the handle and released)
  - `input` works with every value change

</details>

## 16 - Async JavaScript (promises and callbacks, async/await)

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

## Notes
<details>
<summary>Other</summary>

- cycle is more optimal than a recursion (call stack overflow), any recursion could be rewritten into a cycle

</details>