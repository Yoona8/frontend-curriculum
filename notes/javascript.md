# JavaScript
- [Basic definitions](#basic-definitions)
- [Good practices](#good-practices)
- [Code style](#code-style)
- [Constants and variables](#constants-and-variables)
- [Data types and structures](#data-types-and-structures)
- [Numbers](#numbers)
- [Strings](#strings)
- [Iterables](#iterables)
- [Iterables: Arrays](#iterables-arrays)
- [Iterables: Sets and WeakSets](#iterables-sets-and-weaksets)
- [Iterables: Maps and WeakMaps](#iterables-maps-and-weakmaps)
- [Objects](#objects)
- [Functions](#functions)
- [Scope](#scope)
- [Constructors and prototypes](#constructors-and-prototypes)
- [Classes](#classes)
- [Expressions, Control structures and Operators](#expressions-control-structures-and-operators)
- [Modules](#modules)
- [Window Object](#window-object)
- [DOM](#dom)
- [Events](#events)
- [Timers and intervals](#timers-and-intervals)
- [Async JavaScript](#async-javascript-promises-and-callbacks-asyncawait-http-requests)
- [Forms](#forms)
- [Authorization](#authorization)
- [Working with data](#working-with-data)
- [Loading scripts to the page](#loading-scripts-to-the-page)
- [Location API](#location-api)
- [History API](#history-api)
- [Navigator API](#navigator-api)
- [Browser storage](#browser-storage)
- [Service Workers, Web Workers and Worklets](service-workers-web-workers-and-worklets)
- [Meta-programming](#meta-programming)
- [Performance and optimizations](#performance-and-optimizations)
- [Security](#security)
- [Regular expressions](#regular-expressions) - refactor the questions
- [Deploying](#deploying)
- [Testing](#testing)
- [Debugging](#debugging)
- [Browser support](#browser-support) - refactor the questions
- [Tools and workflow](#tools-and-workflow) - refactor the questions
- [Libraries](#libraries) - refactor
- [Frameworks](#frameworks) - refactor
- [Resources](#resources) - refactor

## Basic definitions
<details>
<summary>What is API?</summary>

- API (Application Public Interface)
  - a set of available properties and methods to solve a particular task
  - frequent implementation - objects

</details>

<details>
<summary>What is a dynamically typed variable?</summary>

- can store any value at any time (even when reassigning)
```JavaScript
// types are not set explicitly
let a = 10;
a = 'text';
```

</details>

<details>
<summary>What are statements?</summary>

- syntax constructs and commands that perform actions
- can be separated with `;`
- usually written on separate lines
```JavaScript
console.log('Hello!');
```

</details>

<details>
<summary>What is operand?</summary>

- what operators are applied to: 5 * 2 there are two operands: the left operand is 5 and the right operand is 2 (sometimes called arguments instead of operands)

</details>

<details>
<summary>What are unary, binary and ternary operators?</summary>

- unary - single operand
- binary - has 2 operands
- ternary - has 3 operands

</details>

<details>
<summary>What does alert() do?</summary>

- shows a message

</details>

<details>
<summary>What does prompt() do?</summary>

- shows a message asking the user to input text
- returns the text or, if `Cancel` button or `Esc` is clicked, `null`
```JavaScript
// undefined in the input in IT
const name = prompt('What is your name?');
// for IE
const name = prompt('What is your name?', '');
// preset input (optional)
const name = prompt('What is your name?', 'Dia');
```

</details>

<details>
<summary>What does confirm() do?</summary>

- shows a message and waits for the user to press `OK` or `Cancel`
- returns `true` for `OK` and `false` for `Cancel`/`Esc`

</details>

## Good practices
<details>
<summary>What values is better to pass as arguments and why?</summary>

- don't pass the reference type, pass the id when possible (primitive value)

</details>

## Code style
<details>
<summary>Where are semi-colons placed?</summary>

- Semi-colons `;` are placed after every expression except blocks of code `{}` (exceptions are objects and everything declared with `var`, `let` or `const`, basically variables)

</details>

## Constants and variables
<details>
<summary>What were the issues with var?</summary>

- bad practice (not allowed with `'use strict';`)
```JavaScript
// works without strict mode
name = 'Mary';
// converted into
var name = 'Mary';
```
- hoisting
- recreating
```JavaScript
var i = 21;
// ... some code here
var i = 45;
```
- function and global scope (but no block scope)
- reserved names usage (not allowed with `'use strict';`)
```JavaScript
var undefined = 67;
```

</details>

<details>
<summary>What are the differences between vars, lets and consts?</summary>

- `let`, `const` - no hoisting, no recreating, block scope, using reserved names is not allowed
```JavaScript
// not any const = constant
// declares a variable with immutable link
const element = document.querySelector('p');
const arr = [1, 2, 3, 4];
```

</details>

<details>
<summary>How to declare different types of immutable constants?</summary>

  <details>
  <summary>Primitive value</summary>

  - immutable (code agreement: protected, hardcoded) constant primitive value (physical constants, coefficients, etc)
  ```JavaScript
  const LIGHT_SPEED = 255792458;
  ```

  </details>
  
  <details>
  <summary>Immutable constant array</summary>

  ```JavaScript
  const DEFAULT_NAMES = ['Michael', 'Anna', 'Chris'];
  ```

  </details>

  <details>
  <summary>Enumeration</summary>

  - enumeration (immutable constant) is a complete list of constants grouped by some sign
  ```JavaScript
  const Code = {
    SUCCESS: 200,
    CACHED: 302,
    NOT_FOUND: 404,
    SERVER_ERROR: 500
  };
  ```

  </details>

  <details>
  <summary>Immutable constant object</summary>

  ```JavaScript
  const Earth = {
    RADIUS: 6.371,
    GRAVITATION: 6.67408
  };
  ```

  </details>

</details>

<details>
<summary>Learn more</summary>

- [Let on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
- [Const on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)

</details>

## Data types and structures
<details>
<summary>What data types are available?</summary>

```JavaScript
// 1 - undefined
console.log(typeof undefined); // => undefined
// 2 - null
console.log(typeof null); // => object
// 3 - Boolean
console.log(typeof false); // => boolean
// 4 - Number
console.log(typeof 10); // => number
// 5 - String
console.log(typeof 'text'); // => string
// 6 - Symbol
console.log(typeof Symbol('sym')); // => symbol
// 7 - Object
// iterable lists: Array
// collections: NodeList, HTMLElementsList, classList, arguments
// iterable dictionaries: Map, WeakMap
// iterable sets: Set, WeakSet
// function is also an object, but of type function
console.log(typeof {}); // => object
console.log(typeof []); // => object
console.log(typeof function() {}); // => function
// 8 - BitInt
console.log(typeof 1n); // => bigint
console.log(typeof BigInt(9)); // => bigint
console.log(typeof BigInt('9')); // => bigint
```

</details>

<details>
<summary>What is a typeof operator and how to use it?</summary>
- returns the type of the argument

```JavaScript
typeof undefined; // => undefined
typeof(Symbol('id')); // => symbol
typeof Math; // object
```

</details>

## Numbers
<details>
<summary>How are the numbers stored?</summary>

- every number is a float
- numbers are stored as 64 Bit Floating Points (some issues and limits)

</details>

<details>
<summary>What system JS uses to work with numbers?</summary>

- JS works with binary numbers and converts into decimal

</details>

<details>
<summary>What are the maximum and infinite numbers?</summary>

```JavaScript
// infinite number
1 / 0; // => Infinity
// max numbers
Number.MAX_SAFE_INTEGER; // 2^53 - 1
Number.MIN_SAFE_INTEGER; // -(2^53 - 1)
// floats
Number.MAX_VALUE;
// > or < calculations won't work, only display
// if we do such calculations, no errors
// but strange results because of binary system
```

</details>

<details>
<summary>What are the strange number cases and why do they occur?</summary>

- because JS works with binary and converts into decimal, there are some strange cases
```JavaScript
0.2 + 0.4 === 0.6; // => false (0.6000...1)
// something similar to 1/3 happens (0.33333(3))
(1).toString(2); // => 1
(5).toString(2); // => 101
(1/5).toString(2); // => 0.001100110011...
(0.2).toString(2); // => 0.001100110011...
0.2; // => 0.2
0.2.toFixed(20); // => 0.2000...1110
```

</details>

<details>
<summary>How does BigInt work and when do we use it?</summary>

- to work with > max or < min numbers
- only integer, decimal => error
```JavaScript
// to create add n
9007199254740991985392n;
10n;
// can't mix with numbers
10n - 5; // => error
// but can use like this
10n - 5n; // => 5n
parseInt(10n) - 5; // => 5
10n - BigInt(5); // => 5n
// omits decimal
5n / 2n; // => 2n (not 2.5n)
```

</details>

<details>
<summary>How to convert to a number?</summary>

```JavaScript
Number(undefined); // => NaN
Number(null); // => 0
Number(false); // => 0
Number(true); // => 1
Number('1'); // => 1
Number(' 1 '); // => 1
Number(' \t 1 \n '); // => 1
Number('1s'); // => NaN
```

</details>

<details>
<summary>Learn more</summary>

- [ ] [Number on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)

</details>

## Strings
<details>
<summary>How to check if a string contains some text?</summary>

```JavaScript
const playerName = 'Harry Potter';

// case sensitive
console.log(playerName.includes('rr')); // => true
console.log(playerName.includes('h')); // => false
```

</details>

<details>
<summary>How to remove duplicates?</summary>

- easy way is to convert into an array and use `Set`

</details>

## Iterables
<details>
<summary>What is an iterable (and examples)?</summary>

- objects that implement the 'iterable' protocol (have an `@@iterator` method (ex: `Symbol.iterator`))
- basically objects where you can use `for ... of` loop
- Array, NodeList, String, Map, Set, etc.

</details>

<details>
<summary>What are the characteristics of an array?</summary>

- store data of any kind and length
- has many special methods
- order is guaranteed
- duplicates are allowed
- index-based access

</details>

<details>
<summary>What are the characteristics of a set?</summary>

- store data of any kind and length
- has own special methods
- order is not guaranteed
- duplicates are not allowed
- no index-based access

</details>

<details>
<summary>What are the characteristics of a map?</summary>

- store key-value data of any kind and length
- any key values are allowed
- has own special methods
- order is guaranteed
- duplicate keys are not allowed
- key-based access

</details>

<details>
<summary>Learn more</summary>

- [7 Tips to Handle undefined in JavaScript](https://dmitripavlutin.com/7-tips-to-handle-undefined-in-javascript/)
- [Array vs Set vs Map vs Object — Real-time use cases in Javascript](https://codeburst.io/array-vs-set-vs-map-vs-object-real-time-use-cases-in-javascript-es6-47ee3295329b)
- [Iteration protocols on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols)

</details>

## Iterables: Arrays
<details>
<summary>How to create an Array?</summary>

```JavaScript
// ES5
// 1
var numbers = new Array(3, 5); // => [3, 5]
var emptyArray = new Array(3); // => [] with length === 3
// 2
var numbers2 = Array(3, 5);
var emptyArray2 = Array(3);
// 3
var letters = ['a', 'r']; // => ['a', 'r']
// 4 clones array and adds values from another array
const newNumbers = numbers.concat([8, 5, 2]);

// ES6+
// 5 makes an array of any iterable (collection, separate values)
const elements = Array.from(document.querySelectorAll('li'));
const letters = Array.from('string');
// 6 of separate values
const values = Array.of(1, 2, 3);
// 7
const items = [...elements, ...values];
```

</details>

<details>
<summary>What if we leave some values empty in the middle?</summary>

```JavaScript
const numbers = [1, 2, 5];

// items in between will be empty of undefined value
numbers[5] = 23;
```

</details>

<details>
<summary>How to make an Array of a string?</summary>

```JavaScript
const text = 'One two three';
const words = text.split(' '); // => ['One', 'two', 'three']
const symbols1 = Array.from(text); // => ['O', ..., ' ', 't', ...]
const symbols2 = [...text]; // => ['O', ..., ' ', 't', ...]
```

</details>

<details>
<summary>How to make a string of an Array?</summary>

```JavaScript
const words = ['one', 'two', 'three'];
// by default separates with ,
const text = words.join();
const text2 = words.join(' ');
```

</details>

<details>
<summary>How to check if the Array includes some item?</summary>

```JavaScript
const numbers = [1, 2, 5];
// the same numbers.indexOf(5) !== -1
const isNumberInNumbers = numbers.includes(5);
```

</details>

<details>
<summary>How to get the index of an item in an Array?</summary>

```JavaScript
// if several same values => returns the index of the first
const index = numbers.indexOf(5);
// if several same values => returns the index of the last
const lastIndex = numbers.lastIndexOf(5);
```

</details>

<details>
<summary>How to delete or add an element from (to) an Array at the start or the end?</summary>

- change the initial array
```JavaScript
const numbers = [1, 2, 5];
// add/remove to the end/last of the array
const newNumbersLength = numbers.push(7, 9);
const newNumbersLength2 = numbers.push(...numbers);
const removedItem = numbers.pop();
// add/remove first, slower than push and pop
const newNumbersLength3 = numbers.unshift(9, 12, 15);
const newNumbersLength4 = numbers.unshift(...numbers);
const removedItem2 = numbers.shift();
```

</details>

<details>
<summary>How to delete or add an element from (to) an Array at any position?</summary>

- change the initial array
```JavaScript
const numbers = [1, 2, 5];
// start index, delete count, value to add (or more 10, 15)
const removedElements = numbers.splice(1, 0, 10); // => [1, 10, 2, 5]
// removes from the end
const removedElements2 = numbers.splice(-1, 1); // => [1, 2]
// will delete all items starting with the provided index
const removedElements3 = numbers.splice(0);
```

</details>

<details>
<summary>How reverse items in an Array?</summary>

- change the initial array
```JavaScript
const numbers = [1, 2, 5];
const reversedNumbers = numbers.reverse();
```

</details>

<details>
<summary>What iteration method do we use to iterate over the whole Array and don't need to create something of the Array?</summary>

- doesn't change the initial array
```JavaScript
const numbers = [1, 2, 5];
numbers.forEach();
```

</details>

<details>
<summary>How to sort items in an Array?</summary>

- changes the initial array
```JavaScript
const numbers = [1, 2, 5];
// by default converts to a string and sorts characters
const sortedDefault = numbers.sort();
const sortedNumbers = numbers.sort((a, b) => {
  if (a > b) {
    // or any positive value
    return 1;
  } else if (a === b) {
    return 0;
  } else {
    // or any negative value
    return -1;
  }

  // or
  return a - b;
});
```

</details>

<details>
<summary>How to copy an Array or a part of it?</summary>

- returns a new array
```JavaScript
const numbers = [1, 2, 5];
// copy an array
const clonedNumbers = numbers.slice();
// copy starting from index till the end
const clonedNumbers2 = numbers.slice(2);
// end item not included
const clonedNumbers3 = numbers.slice(0, 2); // => [1, 2]
// [] if nothing is in between
const emptyNumbers = numbers.slice(3, 2);
const emptyNumbers2 = numbers.slice(-3, -4);
// from the end
const clonedPartOfNumbers = numbers.slice(-3, -1); // => [1, 2]
```

</details>

<details>
<summary>How to copy a whole Array and add new items?</summary>

- returns a new array
```JavaScript
const numbers = [1, 2, 5];
// clones array and adds values from another array
const newNumbers = numbers.concat([8, 5, 2]);
```

</details>

<details>
<summary>How to filter the items in an Array?</summary>

- returns a new array
```JavaScript
const numbers = [1, 2, 5];
const filteredNumbers = numbers.filter();
```

</details>

<details>
<summary>How to remove all the falsy values from an array?</summary>

```JavaScript
const arr = [];
const noFalsyArr = arr.filter(Boolean);
```

</details>

<details>
<summary>How to create a new changed Array based on the given Array?</summary>

- returns a new array
```JavaScript
const numbers = [1, 2, 5];
const newTransformedNumbers = numbers.map();
```

</details>

<details>
<summary>How to find an item or an index in an Array?</summary>

```JavaScript
const numbers = [1, 2, 5];
// first element in the array
const number = numbers.find(number => number > 1); // => 2
// index of the first element or -1
const numberIndex = numbers.findIndex(number => number > 1); // => 1
```

</details>

<details>
<summary>How to get the single output value of an Array?</summary>

```JavaScript
const numbers = [1, 2, 5];
const sum = numbers.reduce((prevValue, number, index, numbers) => {
  return prevValue + number;
}, 0);
```

</details>

<details>
<summary>How and why to create a stack using an Array (LIFO)?</summary>

- for tasks, when we have to store previous item (history, browser history, games)
- also available to 'go forward' the history (have to store the removed action back to the stack)
```JavaScript
const questions = [{
  question: 'Which class has a different teacher every year?',
  answers: [{
    answer: 'Defence against the dark arts',
    isCorrect: true
  }, {
    answer: 'Potions',
    isCorrect: false
  }]
}, {
  question: 'What animal represents Hufflepuff house?',
  answers: [{
    answer: 'The Burrow',
    isCorrect: true
  }, {
    answer: 'The Fox',
    isCorrect: false
  }]
}];

const history = [];

const changeQuestion = (newQuestion) => {
  const oldQuestion = questions[0].question;

  questions[0].question = newQuestion;
  
  // store the action (function) and add to the history array
  // works because of closures
  history.push(() => questions[0].question = oldQuestion);
};

console.log(questions[0].question);
changeQuestion('What was the original question?');
console.log(questions[0].question);
changeQuestion('Who is Harry Potter?');
console.log(questions[0].question);

// to get back the stored value
history.pop()();
console.log(questions[0].question);
history.pop()();
console.log(questions[0].question);
```

</details>

<details>
<summary>How and why to create a queue using an Array (FIFO)?</summary>

- for tasks to be executed in a row after some async event
- for unique actions can use `Set` instead of `Array`
```JavaScript
const callbacks = [];

const addAsyncListener = (fn) => {
  // check if the callback exists (used before set was created)
  if (!callbacks.find((it) => it === fn)) {
    callbacks.push(fn);
  }
};

const startAsync = () => {
  setTimeout(() => {
    for (const cb of callbacks) {
      callbacks.delete(cb);
      cb();
    }

    console.log('Done');
  }, 500);
};

const log2 = () => console.log(2);

addAsyncListener(() => console.log(1));
addAsyncListener(log2);
addAsyncListener(log2); // won't be added to array
addAsyncListener(() => console.log(3));

console.log('Start!');
startAsync();

addAsyncListener(() => console.log(4));
addAsyncListener(() => console.log(5));

// the log will be: Start! 1 2 3 4 5 Done
```

</details>

<details>
<summary>Learn more</summary>

- [Array on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [Which Array Function When?](https://dev.to/andrew565/which-array-function-when)
- [map() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
- [find() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
- [findIndex() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)
- [filter() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
- [reduce() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce?v=b)
- [concat() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat?v=b)
- [slice() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
- [splice() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

</details>

## Iterables: Sets and WeakSets
<details>
<summary>How to create a Set and add items?</summary>

```JavaScript
const data = new Set();
// add items
data.add(1);

// based on array or any other iterable
const data = new Set([1, 4, 8]);
```

</details>

<details>
<summary>How to check if the item is in the Set?</summary>

```JavaScript
const isElementInData = data2.has(1); // => true
```

</details>

<details>
<summary>How to delete an item and what if there is no such item?</summary>

```JavaScript
const data = new Set([1, 4, 8]);
// delete not existed item does nothing
data.delete(1);
```

</details>

<details>
<summary>Is a Set an iterable and how to iterate?</summary>

```JavaScript
const data = new Set([1, 4, 8]);
// iterable
for (const item of data) {
  console.log(item);
}
```

</details>

<details>
<summary>What are the entries of a Set?</summary>

```JavaScript
const data = new Set([1, 4, 8]);
const entries = data.entries();

for (const entry of entries) {
  console.log(entry); // => [1, 1] => [4, 4] => [8, 8]
}
```

</details>

<details>
<summary>What is a WeakSet and how is it different from a Set?</summary>

- less methods available
- have to store objects, not primitives
- that's because JS clears those objects (releases to garbage collection) if you don't work with the certain piece of data anymore
```JavaScript
let user = {name: 'Harry'};
const users = new WeakSet();

users.add(user);

// do some operations with user
// still need the set, but not the user
// JS garbage collector will remove the object
// but if we use the Set(), the object (reference type) will not be removed
// from the Set
user = null;
```

</details>

<details>
<summary>Learn more</summary>

- [Set on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)
- [WeakSet on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Weakset)

</details>

## Iterables: Maps and WeakMaps
<details>
<summary>Why a Map, not just an Object?</summary>

- any keys possible
- iterable
- pairs are objects
- better performance (than object) for large quantities of data
- better performance when adding / removing data frequently

</details>

<details>
<summary>How to create a Map and add items?</summary>

```JavaScript
const pairs = new Map();
// add items
pairs.set('John', 'May');
pairs.set('Ichigo', 'Rukiya');

// or with iterable
const pairs = new Map([['John', 'May'], ['Ichigo', 'Rukiya']]);
```

</details>

<details>
<summary>How to get the item from a Map?</summary>

```JavaScript
const pairs = new Map([['John', 'May'], ['Ichigo', 'Rukiya']]);

// get the value
const pair = pairs.get('John');
```

</details>

<details>
<summary>Is a Map an iterable and how to iterate?</summary>

```JavaScript
const pairs = new Map([['John', 'May'], ['Ichigo', 'Rukiya']]);

for (const pair of pairs) {
  console.log(pair); // => ['John', 'May'] => ['Ichigo', 'Rukiya']
}
```

</details>

<details>
<summary>What are the entries, keys, values of a Map?</summary>

```JavaScript
const pairs = new Map([['John', 'May'], ['Ichigo', 'Rukiya']]);

// entries
for (const entry of pairs.entries()) {
  console.log(entry); // => ['John', 'May'] => ['Ichigo', 'Rukiya']
}
for (const [key, value] of pairs.entries()) {
  console.log(key, value);
}

// keys
for (const key of pairs.keys()) {
  console.log(key);
}

// values
for (const value of pairs.values()) {
  console.log(value);
}
```

</details>

<details>
<summary>What is a WeakMap and how is it different from a Map?</summary>

- less methods available
```JavaScript
let user = {name: 'Harry'};
const users = new WeakMap();

users.set(user, 'Some info');

// do some operations with user
// still need the map, but not the user
// JS garbage collector will remove the object
user = null;
```

</details>

<details>
<summary>How to convert an Object into a Map and back from a Map to an Object?</summary>

```JavaScript
const player = {
  name: 'Harry',
  level: 10
};

const playerMap = new Map(Object.entries(player));
const newPlayer = Object.fromEntries(playerMap.entries());
```

</details>

<details>
<summary>Learn more</summary>

- [Map on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
- [WeakMap on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap)

</details>

## Objects
<details>
<summary>What data structures could be used as a key in an Object?</summary>

- strings
- numbers (positive int or floats)
- symbols

</details>

<details>
<summary>Is an Object iterable and how to iterate (not using keys/values/entries)?</summary>

- not iterable (can use `for ... in` old loop, has some issues, not `for ... of`)

</details>

<details>
<summary>How to use an Object as a dictionary (naming convention)? </summary>

```JavaScript
const filterValueToScale = {
  'smallest': 0.25,
  'small': 0.5,
  'normal': 1,
  'large': 2
};
```

</details>

<details>
<summary>How to create an Object (ES5, ES6 creation of the properties)?</summary>

```JavaScript
// ES5
// simple object
const person = {
  'short-name': 'Ron',
  age: 22,
  level: 3,
  3.2: 'some value',
  walk: function() {}
};

// ES6+
// creation with variable
const name = 'Harry';
const user = {
  name,
  level: 1
};
// complex keys (could be useful for dictionaries)
const potter = 'Harry Potter';
const voldemort = 'Tom Riddle';
const antagonist = {
  [potter]: voldemort,
  ['Sirius Black']: 'Bellatrix Lestrange'
};
// new syntax for methods
const character = {
  go() {}
};
```

</details>

<details>
<summary>How the keys of an Object are ordered when logging?</summary>

```JavaScript
const person = {
  'short-name': 'Ron',
  age: 22,
  level: 3,
  3.2: 'some value',
  walk: function() {}
};

// collapsed = not all keys are numbers - not sorted
// collapsed = if all numbers - ascending
// expanded = always sorted, numbers first
console.log(person);
```

</details>

<details>
<summary>How to access the values in an Object?</summary>

```JavaScript
const person = {
  'short-name': 'Ron',
  age: 22,
  level: 3,
  3.2: 'some value',
  walk: function() {}
};

console.log(person.age);
console.log(person['short-name']);
console.log(person[3.2]);
console.log(person['3.2']);
```

</details>

<details>
<summary>What if we access the prop/method which doesn't exist in an object?</summary>

```JavaScript
const person = {
  name: 'Ron',
  age: 22,
  level: 3
};

// if no property or method => undefined (not an error)
console.log(person.hobbies);
```

</details>

<details>
<summary>How to add and use getters and setters?</summary>

```JavaScript
const character = {
  // creation of a property is not required (can be omitted)
  _level: 1,

  // can't use getter/setter + property
  // can't address itself = infinite cycle
  get level() {
    return this._level;
  },
  // always strictly 1 parameter
  set level(value) {
    if (value < 0) {
      this._level = this._level;
      // or set the default value
      // or throw an error
    }
    this._level = value;
  }
};

// addressing the getter or setter
// if there is only setter, can't access the value
const level = character.level;
character.level = 100;
```

</details>

<details>
<summary>How to iterate (entries, values, keys) over an Object?</summary>

```JavaScript
// ES5
// for ... in - deprecated (additional check)

// ES6
// for ... of works if using Symbol.iterator protocol
const player = {
  name: 'Harry',
  level: 10
};
// [['name', 'Harry'], ['level', 10]]
const playerEntries = Object.entries(player);
// ['Harry', 10]
const playerValues = Object.values(player);
// ['name', 'level']
const playerKeys = Object.keys(player);
```

</details>

<details>
<summary>How to add, modify, delete a property or a method of an Object?</summary>

```JavaScript
const player = {
  name: 'Harry',
  level: 10
};

player.age = 33;
player.level = 20;
delete player.name;
```

</details>

<details>
<summary>How to check if the property exists in an Object?</summary>

```JavaScript
const player = {
  name: 'Harry',
  level: 10
};

// but if the property = undefined, also returns false
const hasNameTricky = player.name !== undefined;
// true even if undefined
const hasName = 'name' in player;
// true even if undefined
const hasName2 = player.hasOwnProperty('name');
```

</details>

<details>
<summary>How to copy an Object?</summary>

- not a deep copy
```JavaScript
const player = {
  name: 'Harry',
  level: 10
};

// {} - where
// player - what
const newPlayer = Object.assign({}, player);
// for several
const newPlayer = Object.assign({}, player, {options: 'code'});

// ES6
const newPlayer = {...player};
```

</details>

<details>
<summary>How to deep copy an object?</summary>

- copying deep - recursive with checking typeof function or object
  - lodash has deep copy
  - also there is a hack with `json.parse`, `json.stringify`

</details>

<details>
<summary>How to work with Object Descriptors?</summary>

```JavaScript
const character = {
  name: 'Harry',
  printName: function() {
    console.log(this.name);
  }
};

const descriptors = Object.getOwnPropertyDescriptors(character);
Object.defineProperty(character, 'name', {
  // defaults
  // can delete or define property
  configurable: true,
  // is accessible in for ... in loop
  enumerable: true,
  value: character.name,
  // can rewrite
  writable: true
});

// if writable === false
// no error but won't change, stays the same (Harry)
character.name = 'Ron';

// if configurable === false
// no error but won't delete, stays the same (Harry)
// can't reset configuration also, be careful
delete character.name;

// if enumerable === false
for (const key in character) {
  // will skip the name key, logs only printName
  console.log(key);
}
```

</details>

<details>
<summary>Learn more</summary>

- [ ] [ES6 in Action: Enhanced Object Literals](https://www.sitepoint.com/es6-enhanced-object-literals/)
- [ ] [Objects on MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects)
- [ ] [Object.create on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create)

</details>

## Functions
<details>
<summary>What does function without `return` statement or with empty `return` return?</summary>

- function without `return` statement or with empty `return` returns `undefined`

</details>

<details>
<summary>How to use the return with a long expression?</summary>

```JavaScript
// not like this
// transfers into return;
return
  a + b;

// use ()
return (
  a + b
);
```

</details>

<details>
<summary>What is the difference between parameters and arguments?</summary>

- parameters are variables, which are specified when defining a function
```JavaScript
function printMsg(msg) {}
```
- arguments are the concrete values passed to a function when calling it
```JavaScript
printMsg('Some message');
```

</details>

<details>
<summary>What if the argument is not provided?</summary>

- its value becomes `undefined`

</details>

<details>
<summary>What will be the function name in the console error if thrown from an anonymous function?</summary>

- when there is an error inside the anonymous function, name of the function will be `<anonymous>`
```JavaScript
button.addEventListener('click', function() {});
```
- the only case why to add a name to anonymous function is for debugging, in that case the name of the function will be specified
```JavaScript
button.addEventListener('click', function onClick() {});
```

</details>

<details>
<summary>What are the default parameters of a function and how to use them?</summary>

```JavaScript
// ES5
var doSomething = function (caption, amount, isChecked) {
  if (typeof isChecked === 'undefined') {
    isChecked = false;
  }
};

// ES6
// even if we explicitly pass instead of isChecked undefined,
// the default value will be assigned
const doSomething = (caption, amount, isChecked = false) => {
  // some code here
};

// can also use the previous parameter in default value assignment
const doSomething = (amount, isChecked = amount > 5 ? true : false) => {};
```

</details>

<details>
<summary>How to set up the parameter validation with default parameters?</summary>

```JavaScript
const isRequired = () => {
  throw new Error('The parameter is required!');
};

const doSomething = (text = isRequired()) => {};
```

</details>

<details>
<summary>What are the differences between Function Declaration and Function Expression?</summary>

- the syntax is different
- declaration 'bubbles' (can be used before the declaration), expression is created when the execution flow reaches it
- in strict mode, when a declaration is within a code block, it's visible everywhere inside that block but not outside
```JavaScript
const age = 18;

if (age < 18) {
  function sayHello() {
    console.log('Hello!');
  }
} else {
  function sayHello() {
    console.log('Welcome!');
  }
}

sayHello(); // error (not defined)
```

</details>

<details>
<summary>What are the arrow functions and how do they differ from a normal function?</summary>

- doesn't have it's own scope (only lexical) - when global, `this === window`
- doesn't have `arguments` object
- can't rewrite `this` (`bind` and `call` won't work)
  - can't be used as a constructor, no `new` keyword
  - can't be method of an object or prototype

```JavaScript
// only 1 param?
const doSomething = param => console.log(param);

// only 1 expression?
// = return left * right;
const doSomething = (left, right) => left * right;

// return object?
const getWizard = (name, level) => ({
  name,
  level
});
```

</details>

<details>
<summary>What is the arguments keyword in a function?</summary>

- don't have to pass as a parameter (accessible as a keyword inside any function)
- iterable structure

</details>

<details>
<summary>What do bind, call, apply do and how are they different?</summary>

- `call` (values) and `apply` (array) call the function (as `()`)
- `bind` doesn't call the function
- the arguments passed after context are preset arguments, when the arguments are passed on function call, append to the end
```JavaScript
const addNumbers = (cb, ...numbers) => {
  // sum numbers
  let result = 100;

  cb(result);
};

const printResult = (text, result) => console.log(`${text} ${result}`);

addNumbers(printResult.bind(this, 'The sum is:'), 10, 90);
```
- more info in [scope](#scope) section

</details>

<details>
<summary>How to call a function with template literals (tagged templates)?</summary>

- with tagged template literals the value of the first argument is always an array of the string values, the remaining arguments are of the passed expressions
```JavaScript
const getPlayerInfo = (first, second, third) => {
  console.log(first); // ['', ' is ', ' for now']
  console.log(second); // 'Harry'
  console.log(third); // 10
};

const name = 'Harry';
const level = 10;

getPlayerInfo`${name} is ${level} for now`;
```

</details>

<details>
<summary>What are pure functions and the side effects?</summary>

- for the same input always give the same output
- no side effects
```JavaScript
// pure function
const addNumbers = (num1, num2) => {
  return num1 + num2;
};

// impure - output changes
const addRandomNumber = (num) => {
  return num + Math.random();
};

// impure - side effect
let result = 0;

const addNumber = (num) => {
  result += num;
  return result;
};

// impure - side effect
const books = ['If I Never Met You', 'Atomic Habits'];

const addBook = (book) => {
  books.push(book);
};
```

</details>

<details>
<summary>What are factory functions and why to use them?</summary>

- functions which create a function
- good for pre-configuring some values
```JavaScript
// for not to pass the tax rate all the time
const createCalculateTax = (tax) => {
  return (amount) => {
    return amount * tax;
  };
};

const calculateVatAmount = createCalculateTax(0.19);
const calculateIncomeTaxAmount = createCalculateTax(0.25);

console.log(calculateVatAmount(100));
console.log(calculateIncomeTaxAmount(100));
```

</details>

<details>
<summary>What are closures?</summary>

- all functions in JS are closures
- function locks in all surrounding variables
- mostly used for factory functions

</details>

<details>
<summary>What is a recursion and why to use it?</summary>

- sometimes it's shorter than other ways
- if too many calls => stack overflow
```JavaScript
const getPower = (a, n) => {
  let result = 1;

  for (let i = 0; i < n; i++) {
    result *= a;
  }

  return result;
};

const getPowerRec = (a, n) => {
  // don't forget to add an exit condition
  if (n === 1) {
    return a;
  }

  return a * getPowerRec(a, n - 1);
};

// even shorter
const getPowerRec = (a, n) => {
  return n === 1 ? a : a * getPowerRec(a, n - 1);
};
```
- where do we need the recursion?
- when there are some nested objects but we don't know exactly how many
```JavaScript
const player = {
  name: 'Harry',
  teamMembers: [{
    name: 'Ron',
    teamMembers: [{
      name: 'Ginny'
    }]
  }, {
    name: 'Hermione',
    teamMembers: [{
      name: 'Luna',
      teamMembers: [{
        name: 'Mary'
      }]
    }]
  }, {
    name: 'Sirius'
  }, {
    name: 'Ellie'
  }]
};

const getTeamMemberNames = (player) => {
  const names = [];

  if (!player.teamMembers) {
    return [];
  }

  for (const teamMember of player.teamMembers) {
    names.push(teamMember.name);
    names.push(...getTeamMemberNames(teamMember));
  }

  return names;
};

console.log(getTeamMemberNames(player));
```

</details>

<details>
<summary>Learn more</summary>

- [Functions on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)
- [Bind on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind)
- [Closures on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
- [Recursion on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions#Recursion)
- [Tagged templates on  MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_templates)
- [Arrow functions on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [Arrow function expressions on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions#No_binding_of_this)

</details>

## Scope
<details>
<summary>What is a scope and a context?</summary>

- scope is where the function runs
- context depends on how the function is called
- while the function is not called, it doesn't have any context
- context is being created upon the function call

</details>

<details>
<summary>What is `this` and how to change it?</summary>

- it is a context
- created upon the function call
- depends on how the function is called
- could be changed, also with `apply`, `call`, `bind`

</details>

<details>
<summary>How does `use strict` affect `this` keyword?</summary>

- no `use strict`, `this` = `window`, with `this` = `undefined` (for global this inside the function)

</details>

<details>
<summary>What is `this` inside an Object?</summary>

- in an object (method) `this` is the reference to the object itself (but remember, in depends on how the function is called)

</details>

<details>
<summary>What will be `this` in case of outer function (call on object and in global scope)?</summary>

```JavaScript
const walk = function() {
  console.log(this + 'walk!');
};

const player = {
  name: 'Ron',
  walk
};

// this links to player object
player.walk();
// TypeError: Cannot read property '...' of undefined
walk();
```

</details>

<details>
<summary>What will be `this` if we use destructuring and call the function in the global scope?</summary>

```JavaScript
const player = {
  name: 'Harry',
  age: 28,
  run() {
    console.log(this + ' runs!');
  }
};

const { run } = player;
// TypeError: Cannot read property '...' of undefined
run();
```

</details>

<details>
<summary>What if we use closures inside the object method?</summary>

- with closure the result is more obvious
```JavaScript
const guitarPlayer = {
  firstName: 'Michael',
  lastName: 'Lantsov',
  play() {
    console.log(`${guitarPlayer.firstName} ${guitarPlayer.lastName}`);
  }
};

const anotherPlayer = {
  firstName: 'Anna',
  lastName: 'Starkov'
  play: guitarPlayer.play
};

// output will be the same
guitarPlayer.play();
anotherPlayer.play();
```

</details>

<details>
<summary>What is `this` in an instance of a class or when using a constructor function?</summary>

- `this` refers to current instance of an object in a `class`
- binds `this` in the constructor

</details>

<details>
<summary>What is the issue with using array methods inside the object methods and `this`?</summary>

```JavaScript
const players = {
  team: 'Griffindor',
  members: ['Harry', 'Ron', 'Hermione'],
  getMembers() {
    this.members.forEach(function(member) {
      // here this is created when the forEach calls it
      // it is called not on players object
      // so this here === global scope or undefined
      // could be solved with arrow function
      console.log(this);
    });
  }
};
```

</details>

<details>
<summary>How and why do we use `bind`, `call` and `apply`?</summary>

- `bind` creates a new function, the initial function stays the same
- `bind` context can't be changed even with `apply` and `call`
```JavaScript
// here `this === obj` instead of `a` (respects the first binding)
obj.getThis4 = obj.getThis2.bind(obj);
obj.getThis4.call(a);
```
- calling a function with bound context (1st param in those functions is always context, the 2nd parameter differs)
```JavaScript
// arguments separated with ',' will be function params
// perfect when there are not many params
play.call(anotherPlayer, '20.02.1967');
// array, which values will be function params
// good for many params or undefined number of params
play.apply(guitarPlayer, ['20.02.1967']);
```
```JavaScript
const numbers = [1, 3, 100, 5];

// we don't need context here, so pass 'null'
console.log(Math.max.apply(null, numbers));
```

</details>

<details>
<summary>What is the context inside the event listener?</summary>

- listener's context is always === the element, to which the listener is applied `document.body` or `evt.currentTarget` (the browser binds `this` (on event listeners) to the DOM element that triggered the event)
```JavaScript
// even in this case
const cart = {
  item: 'Book',
  price: 6,
  print() {
    console.log(`${this.item} \$${this.price}`)
  }
};

item.addEventListener('click', cart.print);
// browser will store the function
item.callback = cart.print;
// and executes the callback
// so just won't work (because it's not cart.callback(), but callback())
item.callback();
```
- can override if create the event handler and execute the method
```JavaScript
item.addEventListener('click', function() {
  cart.print();
});
```
- with bind (but careful, `bind` returns a new function, store first in a separate variable to unsubscribe if needed)
```JavaScript
// can't remove the listener
item.addEventListener('click', cart.print.bind(cart));

// to remove a listener
const printCart = cart.print.bind(cart);

item.addEventListener('click', printCart);
item.removeEventListener('click', printCart);
```
```JavaScript
// custom binder (like the bind works)
const customBind = function(fn, context) {
  return function() {
    return fn.apply(context, arguments);
  };
};
```

</details>

<details>
<summary>What are the differences of scope related to arrow functions?</summary>

- arrow functions do not have their own context (even when we use `call`, `apply` or `bind`)
- arrow functions passed as a callback to event listeners also have no context
- even with strict mode `this` won't be undefined but referred to the global scope (arrow functions do not have `this` property)
- arrow functions **NEVER** have their own context
```JavaScript
const players = {
  team: 'Griffindor',
  members: ['Harry', 'Ron', 'Hermione'],
  getMembers() {
    this.members.forEach((member) => {
      // works fine because arrow function
      // doesn't bind this
      // so this is the same as in getMembers function
      console.log(member, this.team);
    });
  }
};

players.getMembers();
```

</details>

<details>
<summary>Learn more</summary>

- [this on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- [What is `this`? The Inner Workings of JavaScript Objects](https://medium.com/javascript-scene/what-is-this-the-inner-workings-of-javascript-objects-d397bfa0708a)

</details>

## Constructors and prototypes
<details>
<summary>What is `__proto__` of an Object constructor?</summary>

- base `Object` doesn't have a `__proto__`

</details>

<details>
<summary>When the constructor prototype is assigned?</summary>

- constructor prototype is assigned to the instance upon creation

</details>

<details>
<summary>Where does prototype exist? (On what type of object?)</summary>

- `prototype` property exists only on function object

</details>

<details>
<summary>How the prototype chain works?</summary>

```JavaScript
const Player = function(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
};

// == extends in classes
Player.prototype.play = function() {};

const harryPotter = new Player('Harry', 'Potter');
const ronWeasley = new harryPotter.__proto__.constructor('Ron', 'Weasley');

// first looks inside the instance
// than in Player prototype (harryPotter.__proto__.play())
harryPotter.play();
console.log(harryPotter.__proto__ === Player.prototype); // => true
// than in the Player's prototype's prototype
// till it reaches the Object.prototype
// harryPotter.__proto__.__proto__.toString();
harryPotter.toString();
```

</details>

<details>
<summary>How to create and use a constructor function?</summary>

- naming `Player`
- creation of an instance with `new` keyword
- add a method to the prototype
```JavaScript
const Player = function(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
};

// to add a static method
Player.describe = function() {
  console.log('Creating players.');
};

// __proto__: { play: function() {} }
Player.prototype.play = function() {};

// will add method to object Player
// available Player.play() only
// if called on instance = TypeError
Player.play = function() {};

const harryPotter = new Player('Harry', 'Potter');
```

</details>

<details>
<summary>What the `new` keyword does?</summary>

- `new` keyword doesn't call the function, it creates an object with it's fields (when we use `this.name = name`)
```JavaScript
const Player = function(firstName, lastName) {
  // new 'creates' this as an object
  this = {};
  // adds properties and methods
  this.firstName = firstName;
  this.lastName = lastName;
  this.greet = function() {
    console.log(`Hello! I'm ${this.firstName} ${this.lastName}`);
  };
  // returns the object
  return this;
};
```

</details>

<details>
<summary>What if we try to create an instance without the `new` keyword?</summary>

- without `new` => `undefined` (void = return undefined) will not be created
```JavaScript
const ron = Player('Ron', 'Weasley'); // undefined, not created
```

</details>

<details>
<summary>How to check if the instance was created with a `new` keyword?</summary>

```JavaScript
// ES6+
const Player = function(firstName, lastName) {
  if (!new.target) { 
    throw new Error('Should be called with new operator.'); 
  }
};
```

</details>

<details>
<summary>How to check what constructor was used to create an instance?</summary>

```JavaScript
console.log(harryPotter instanceof Player); // => true
```

</details>

<details>
<summary>Why `new` if we can just return an object or this?</summary>

- `instanceof` becomes useless
- inheritance (prototype) won't work
- if you try to imitate a constructor and `return this;`, `this` would be a global object

</details>

<details>
<summary>Learn more</summary>

- [Prototypal Object-Oriented Programming using JavaScript](https://alistapart.com/article/prototypal-object-oriented-programming-using-javascript/)
- [Inheritance in JavaScript on MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Inheritance)

</details>

## Classes
<details>
<summary>How to create a class and what method is better?</summary>

- `class` better than `const` when creating a class
```JavaScript
class Player {
  // is optional
  // helps to create an instance of a class
  constructor() {}

  // for every instance
  onClick = () => {}

  // inside prototype
  play() {}
}

// don't create classes like this
const Singer = class {};
```

</details>

<details>
<summary>What are properties and fields of a class and are they different?</summary>

- properties and fields are basically the same thing
```JavaScript
class Player {
  // fields (still poor support)
  // for now use methods only
  // and add all the properties inside of constructor
  level = 2;

  // all properties are defined here
  constructor(name) {
    // properties
    this.name = name;
    this.onButtonClickArrowFn = () => {
      // this === current instance of a class
      console.log(this);
    };
  }
}

```

</details>

<details>
<summary>How to create an instance of a class?</summary>

- `new` for creating an instance (or type error due to built-in `new.target` check)
```JavaScript
const player = new Player('Harry');
```

</details>

<details>
<summary>What if you try to access the field or property which is not defined in the class?</summary>

- `undefined`

</details>

<details>
<summary>Can we use getters and setters in a class?</summary>

- getters / setters can be used

</details>

<details>
<summary>How to add private fields?</summary>

- private fields, soon to use `this.#skill = value;`

</details>

<details>
<summary>How to deal with event listeners if we need `this` reference to an instance of a class?</summary>

```JavaScript
class Player {
  constructor() {
    this.onButtonClickArrowFn = () => {
      // this === current instance of a class
      console.log(this);
    };
  }

  onButtonClick() {
    console.log(this);
  }

  play() {
    // this === button
    button.addEventListener('click', this.onButtonClick);
    // this === current instance of a class
    button.addEventListener('click', this.onButtonClick.bind(this));
    button.addEventListener('click', () => this.onButtonClick());
    // but is created for every instance
    button.addEventListener('click', this.onButtonClickArrowFn);
  }
}

```

</details>

<details>
<summary>How do classes actually work (under the hood)?</summary>

```JavaScript
class Person {}

// extends works like a __proto__
// Player.__proto__ === Person.prototype
class Player extends Person {
  name = 'Harry';

  constructor() {
    super();
    this.age = 33;
    // if created like this => part of any instance (like a property)
    this.play = function() {};
  }

  // methods are added to prototype
  greet() {
    console.log(`Hi! My name is ${this.name}.`);
  }

  // if created like this => part of any instance (like a field/property)
  play = function() {};
  // if we use an arrow function here, context will stay the same
  // even when added as an event handler (don't have to bind)
  play = () => {};
}
```

</details>

<details>
<summary>How to create static properties, fields and methods?</summary>

- properties can also be static (but still poor browser support)
- not inherited, accessible on a class without instantiation
```JavaScript
class Player {
  constructor(level, weaponsCount) {
    this.level = level;
    this.weaponsCount = weapons;
  }

  static createJuniorPlayer() {
    return new this(5, 2);
  }
}

const juniorPlayer = Player.createJuniorPlayer();
```

</details>

<details>
<summary>What are the differences between a class and a constructor function?</summary>

- `class` can't be used without `new` (could be imitated inside the constructor function with `new.target`)
- class methods are not iterable
```JavaScript
for (const prop in player) {
  console.log(prop);
}
```

</details>

<details>
<summary>Learn more</summary>

- [ ] [OOP notes](./oop.md)
- [ ] [Classes on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
- [ ] [ES6 Classes in Depth](https://ponyfoo.com/articles/es6-classes-in-depth)

</details>

## Expressions, Control structures and Operators
<details>
<summary>What are the basic math operators?</summary>

- `=`
 ```JavaScript
// assignment returns a value
// x = value writes the value into x and then returns it
let a = 1;
let b = 2;
let c = 3 - (a = b + 1);

console.log(a); // 3
console.log(c); // 0

// chaining assignment
// evaluate from right to left
// 1. the rightmost expression 2 + 2 is evaluated 
// 2. and then assigned to the variables on the left: c, b and a
let a, b, c;

a = b = c = 2 + 2;
console.log(a); // => 4
console.log(b); // => 4
console.log(c); // => 4
 ```
- `+` or `+=`
- `-` or `-=`
- `*` or `*=`
- `/` or `/=`
- `%`
- `**` exponentiation operator (not supported in IE)
```JavaScript
console.log(2 ** 2); // => 4 (2 pow 2)
console.log(4 ** (1 / 2)); // => square root
console.log(8 ** (1 / 3)); // => cubic root
```

</details>

<details>
<summary>How increment and decrement operators can be applied?</summary>

- only to variables, `5++` will cause an error

</details>

<details>
<summary>What is the difference between postfix and prefix increment and decrement?</summary>

- `return result++;` returns first the result and then increments
- `return --result;` decrements and then returns the changed value
```JavaScript
let initialNumber = 1;
let counter = initialNumber++;
let counter2 = ++initialNumber;
console.log(counter); // => 1
console.log(counter2); // => 2
```

</details>

<details>
<summary>How to use increment and decrement inside the expression?</summary>

```JavaScript
let counter = 1;
console.log(2 * ++counter); // => 4

let counter = 1;
console.log(2 * counter++); // => 2
// if you need multiply and then increase, more readable
console.log(2 * counter);
counter++;
```

</details>

<details>
<summary>What are bitwise operators?</summary>

- treat arguments as 32-bit integer numbers and work on the level of their binary representation
- used very rarely, when we need to fiddle with numbers on the very lowest (bitwise) level
- in some special areas, such as cryptography, they are useful
- AND `&`
- OR `|`
- XOR `^`
- NOT `~`
- LEFT SHIFT `<<`
- RIGHT SHIFT `>>`
- ZERO-FILL RIGHT SHIFT `>>>`

</details>

<details>
<summary>What does comma operator do?</summary>

- allows to evaluate several expressions, dividing them with `,`
- each of them is evaluated but only the result of the last one is returned
```JavaScript
// the first expression 1 + 2 is evaluated and its result is thrown away
// then, 3 + 4 is evaluated and returned as the result
let a = (1 + 2, 3 + 4);
console.log(a); // => 7

// comma operator has very low precedence, lower than =
// so parentheses are important in the example above
// evaluates + first, summing the numbers into b = 3, 7
// then the assignment operator assigns b = 3
// and the rest is ignored
let b = 1 + 2, 3 + 4;
console.log(b); // => 3

// why do we need an operator that throws away everything except the last expr?
// sometimes it is used to put several actions in one line
for (a = 1, b = 2, c = a * b; a < 10; a++) {}
```

</details>

<details>
<summary>What is the difference between `if ... else` and ternary operator?</summary>

- `if ... else` - returns no value
- `? :` - always returns a value

</details>

<details>
<summary>How to use `switch` operator and how does it compare?</summary>

- always uses `===` to compare
```JavaScript
switch (+expression) {
  case value + 1: 
    console.log(value);
    break;
  // grouping cases
  case value2:
  case value3:
    console.log(value2, value3);
    break;
  default:
    // default is optional
    console.log('default');
}
```

</details>

<details>
<summary>What are the 'falsy' values?</summary>

- `0`
- `''`
- `NaN`
- `null`
- `undefined`

</details>

<details>
<summary>What are the 'truthy' values?</summary>

- numbers `!== 0`
- not empty strings (even `'   '` and `'0'`)
- `[]`, `{}` and all other objects and arrays

</details>

<details>
<summary>What are the comparison operators?</summary>

- `==` and `===`
- `!=` and `!==`
- `>` and `<`
- `>=` and `<=`

</details>

<details>
<summary>How does JS compare strings?</summary>

```JavaScript
// JS compares strings based on standard lexicographical ordering (Unicode)
console.log('b' > 'a'); // => true

// JS always looks at the first char and only considers other chars if the 1st
// chars are the same
console.log('ab' > 'aa'); // => true

// uppercase chars are smaller than lowercase
console.log('a' > 'B'); // => true
```

</details>

<details>
<summary>How does JS compare different types (except === and !==)?</summary>

- converts the values to numbers
```JavaScript
console.log('3' > 1); // true
console.log('04' == 4); // true
console.log(true == 1); // true
console.log(false == 0); // true

// the strange thing because of this conversion
const a = 0;
const b = '0';

console.log(Boolean(a)); // false
console.log(Boolean(b)); // true
console.log(a == b); // true
```

</details>

<details>
<summary>How does JS compare with === and !==?</summary>

- compares without type conversion
```JavaScript
console.log(0 === false); // false
```

</details>

<details>
<summary>How to compare with null or undefined?</summary>

```JavaScript
console.log(null === undefined); // false
// special rule for == equal to each other but not to any other value
console.log(null == undefined); // true
// for other math and comparison operator
// null => 0
// undefined => null

// null vs 0 works strange
console.log(null > 0); // false
console.log(null == 0); // false
console.log(null >= 0); // true

// undefined shouldn't be compared to other values
// converted to NaN which returns false for all comparisons
console.log(undefined > 0); // false
console.log(undefined < 0); // false
console.log(undefined == 0); // false
```

</details>

<details>
<summary>What are logical operators?</summary>

- `||` or
- `&&` and
- `!` not (precedence is the highest of all logical)
- `??` nullish coalescing
- can be applied to values of any type
- the result can be of any type

</details>

<details>
<summary>What is `not` operator and how to convert into boolean?</summary>

- `!`
- `!!userName` converts into a boolean

</details>

<details>
<summary>How to use OR and AND, which one is higher?</summary>

- `a && b` if both are true
- `a || b` if at least one is true
- `&&` precedence is higher than `||`
- do not convert value into a boolean
```JavaScript
// returns the 1st falsy value
const userName1 = null && 'Mary'; // => null
// use value if the condition is true
const isLoggedIn = true; // if false => false
const userName0 = isLoggedIn && 'Mary'; // => 'Mary'
// if all are truthy, the last one is returned
const userName2 = 'Lily' && 'Max' && 'Mary'; // => 'Mary'
```
```JavaScript
// default value assignment
// getting the first truthy value from a list of variables or expressions
// returns 1st truthy value
const userName1 = '' || 'Mary' || 'Maya'; // => 'Mary'
const userName2 = 'Max' || 'Mary' || ''; // => 'Max'
// if all falsy, the last value is returned
const userName3 = null || 0 || ''; // => ''

// short-circuit evaluation
true || console.log('Will not be logged!');
false || console.log('Logged!');
```

</details>

<details>
<summary>How does nullish coalescing work and the cases?</summary>

- to provide a default value
```JavaScript
// returns the first argument if it's not `null` or `undefined`
// otherwise the second
const result = user ?? 'Unknown';
// is the same
const result = (user !== null && user !== undefined) ? user : 'Unknown';
// can be used in a sequence
const first = null;
const second = null;
const third = 'Third';
console.log(first ?? second ?? third ?? 'Unknown'); // => Third
// is the same (but for all falsy values)
console.log(first || second || third || 'Unknown');
```

</details>

<details>
<summary>How to use `??` with `&&` or `||`?</summary>

- due to safety reasons, JS forbids using `??` with `&&` and `||` operators unless the precedence is explicitly specified with `()`
```JavaScript
// Syntax error
let text = 'one' && 'two' ?? 'three';
// Works just fine
let text = ('one' && 'two') ?? 'three';
```

</details>

<details>
<summary>How to check if the value is `NaN`?</summary>

- `isNaN()` to check if NaN or not
- `isNaN(value) || value <= 0` if the first part is `true`, JS doesn't go further

</details>

<details>
<summary>How to use destructuring with iterables?</summary>

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
// when we want specific values and an array of the rest
const [first, ...otherNumbers] = numbers;
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
<summary>How to use destructuring with Object?</summary>

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
// creates name and object of remained properties
const {name, ...otherProperties} = cat;

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

<details>
<summary>What is better: loop or recursion?</summary>

- in most cases loop is more efficient than a recursion (call stack overflow)
- any recursion could be rewritten into a loop

</details>

<details>
<summary>What are the general loops?</summary>

- `for (let i = 0; i < 5; i++) {}`
- `for (const item of items) {}`
  - almost the same as `for` loop
  - can use `break` and `continue`
  - could be used with every iterable (not only `Array`)
- `for (const key in someObject) {}`
  - requires additional check, otherwise can go through the whole prototype chain
- `while (isEdit) {}` as long as the condition is true
- `do { ... } while (isEdit);` runs at least once

</details>

<details>
<summary>What do `break` and `continue` do?</summary>

- `break;` stops the loop execution
  - if inside the nested loop - stops only the nested one, outer continues
- `continue;` skips only the current iteration and moves to the next

</details>

<details>
<summary>How and why to use a labeled statement?</summary>

- labeled statements could be used with any expression but mostly used with loops
- to break or continue the outer loop from inner
```JavaScript
outerLoop: for (const item of items) {
  console.log('Outer', item);

  innerLoop: for (let i = 0; i < 5; i++) {
    if (i === 2) {
      break outerLoop;
      // or
      continue outerLoop;
    }

    console.log('Inner', i);
  }
}

// could also break from somewhere else in the code
const button = document.querySelector('.button');

button.addEventListener('click', () => {
  break outerLoop;
  // or
  continue outerLoop;
});
```

</details>

<details>
<summary>How to use rest and spread operators?</summary>

- rest collects several values into one iterable structure
- rest must be last parameter in the function (or error)
```JavaScript
// before
function doSomething() {
  return Array.from(arguments);
}
// with rest
const doSomething = (...values) => {
  return values;
};
// destructuring + rest = first and an array of others
const [first, ...others] = doSomething();
```

```JavaScript
// spread - any iterable into separate values
// before
const values = [1, 2, 40, 73, 5];
// find max
Math.max.apply(null, values);
// merge arrays
const newValues = [];
newValues.concat(values);

// with spread
// find max
Math.max(...values);
// merge arrays
const newValues = [...values];
const filteredValues = [...values].filter();
```

</details>

<details>
<summary>What can be used with the `throw` operator?</summary>

- `throw { message: 'some message' };` can throw anything as an error, not only `new Error()`

</details>

<details>
<summary>When is it good to use `try catch finally`?</summary>

- use `try {} catch (error) {}` only for the code you can't control (ex: server errors, user input)

</details>

<details>
<summary>In what variations can we use `try catch finally`?</summary>

- `try ... catch` or `try ... finally` but never `catch ... finally`

</details>

<details>
<summary>When does `catch` get executed?</summary>

- if `try` doesn't throw an error, `catch` won't be executed

</details>

<details>
<summary>Why to use and when does `finally` run?</summary>

- when we want to throw the error from inside the `catch` block to send to some statistics etc
- some cleanup work (release data, clear the variables, etc)
- if the error is thrown from `catch`, only finally executes, code after `try ... catch ... finally` block won't be executed
- `finally` always runs

</details>

<details>
<summary>How does `try catch finally` work in details?</summary>

```JavaScript
function doSomething() {
  try {
    console.log(0); // => 0
    throw 'error ocurred';
  } catch(error) {
    // error => 'error ocurred' (what was used with 'throw')
    console.log(1); // => 1
    // this return statement is suspended till finally block completes
    return true;
    // not reachable
    console.log(2);
  } finally {
    console.log(3); // => 3
    // overwrites the return from catch block
    // function returns this value
    return false;
    // not reachable
    console.log(4);
  }
  // the function returns false from finally block
  // not reachable 
  console.log(5);
}

console.log(doSomething()); // => 0, 1, 3, false
```

</details>

<details>
<summary>Learn more</summary>

- [Operator precedence](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)
- [Control flow and error handling](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)
- [Loops and iteration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration)
- [For ... of on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
- [Rest on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)
- [Spread on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
- [Destructuring on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
- [Bitwise on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#bitwise_operators)

</details>

## Modules
<details>
<summary>What problems do modules solve?</summary>

- namespace
  - no global scope
  - encapsulation
- dependencies
  - easy to follow on what module depends on
- interface
  - methods and props export, easy to navigate

</details>

<details>
<summary>What methods to write modules were used in ES5 (and what are the downsides)?</summary>

- manual configuration
- have to remember dependencies order
- is not clear, what dependencies are used

```JavaScript
// IIFE
'use strict';
// slider.js
(function() {
  window.slider = {
    name: 'Eve'
  };
})();
```

- better module approaches were found (AMD, CommonJS, UMD)

</details>

<details>
<summary>What about `use strict` inside the module?</summary>

- `'use strict;'` by default

</details>

<details>
<summary>How to create a module?</summary>

- syntax looks like destructuring but not the same
- better export const or class (if you export let, can't reassign in the other module anyway)
- do not fold `export` and `import` into code blocks `{}`
```JavaScript
// module-name.js
// named - names should be the same (or error, module won't get loaded)
// could import not all the export
// can't export the same variable 2x
// better not to combine inline and group exports
export { name, age };
// or
export const name = 'Max';
export const age = 40;
// renamed
export { name as userName };
// default
// better for classes
// could be hard to debug (imported by any name)
export default name;
export default { name };
export { name as default };
```

</details>

<details>
<summary>How to import a module?</summary>

- syntax looks like destructuring but not the same
- imported variable is not created (the same link to the exported variable)
- do not fold `export` and `import` into code blocks `{}`
- no hoisting, so that's why `import` is always on top
```JavaScript
// other-module.js
// import using the same variable name
import { name } from './module-name.js';
// import all as child (ignores default, insecure, have no control on import)
import * as child from './module-name.js';
// renamed
import { name as userName } from './module-name.js';
// default
import name from './module-name.js';
import { default as name } from './module-name.js';
// import without a variable if we only need to execute the code from module
import './log.js';
```

</details>

<details>
<summary>What if we import an inexistent variable or some error occurs while importing a module or children?</summary>

- `import` of inexistent variable = error, module won't get loaded
- if there is an error while downloading the module or its children => all connected modules won't get loaded

</details>

<details>
<summary>What are the dynamic imports?</summary>

- there are dynamic imports, but browser support is still pretty poor

</details>

<details>
<summary>What if you import the same module for several times?</summary>

- even when you import the same module several times, browser loads only once

</details>

<details>
<summary>What paths can be used in imports?</summary>

- both `''` and `""` available
- path is an immutable constant, can't generate the path
- if 2 same imports => browser downloads only one
- paths abs or rel
  - `https://google.com` url
  - `/utils/helpers.js` abs domain-name
  - `./helpers.js` rel
  - `../helpers.js` rel
- `helpers.js` or `utils/helpers.js` is not supported (reserved for libs from package managers)

</details>

<details>
<summary>What are the module loaders?</summary>

- browsers: ES modules in browsers
```HTML
<!-- adding modules to the page -->
<!-- by default works like defer -->
<script type="module">
  // some code here
</script>
<script src="module-1.js" type="module"></script>
<!-- fallbacks (ignored by browsers, which support modules) -->
<script src="module-1.js" nomodule></script>
```
- static: webpack, rollupJS, parcel, ...

</details>

<details>
<summary>What does the module loader do?</summary>

- orders files
- downloads, stores files
- builds, minifies, packs
- all dependencies are loaded relatively to the 1st loaded module
- browser cashes not only a file, but also the result of executing the module + returned values

</details>

<details>
<summary>What is a proxy module?</summary>

```JavaScript
// module-1.js
export { name as nameOne };

// module-2.js
export { name as nameTwo };

// module-3.js
export * from './module-1.js';
export * from './module-2.js';

// module-target.js
import { nameOne, nameTwo } from './module-3.js';
```

</details>

<details>
<summary>Learn more</summary>

- [IIFE](http://benalman.com/news/2010/11/immediately-invoked-function-expression/)
- [What is AMD, CommonJS, and UMD?](https://www.davidbcalhoun.com/2014/what-is-amd-commonjs-and-umd/)
- [AMD](https://github.com/amdjs/amdjs-api/wiki/AMD)
- [Common.js](http://www.commonjs.org/)
- [UMD](https://github.com/umdjs/umd)
- [ECMAScript modules in browsers](https://jakearchibald.com/2017/es-modules-in-browsers/)
- [ES6 In Depth: Modules](https://hacks.mozilla.org/2015/08/es6-in-depth-modules/)
- [ES6 Modules in Depth](https://ponyfoo.com/articles/es6-modules-in-depth)
- [import on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)
- [export on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)
- [Exploring ES6 - 16. Modules](https://exploringjs.com/es6/ch_modules.html)
- [ ] [Modules on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)

</details>

## Window Object
<details>
<summary>What is the `window` object and how do we use it?</summary>

- browser API, contains all the global properties and methods
```JavaScript
// can call both ways
alert('Say something');
window.alert('Say something');
```

</details>

<details>
<summary>Learn more</summary>

- [ ] [Window on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window)

</details>

## DOM
<details>
<summary>What is DOM?</summary>

- a part of `window` object

</details>

<details>
<summary>How does the browser searches through the DOM?</summary>

- browser searches DOM in depths, so that the first tag is being found (otherwise not obvious)

</details>

<details>
<summary>How to select the elements with query methods?</summary>

- if no matching => `null` for single or empty collection
```JavaScript
// any css selector
// returns first matching element in the DOM
document.querySelector('ul li:last-child');
// any css selector
// returns NodeList - static collection (snapshot)
// DOM changes doesn't affect 
// (nodes, not only DOM elements, also text, spaces, etc)
document.querySelectorAll('li');

// all those methods could be called only on document, not on element
document.getElementById('title');
// return HTMLCollection - live collection
document.getElementsByClassName('class');
document.getElementsByTagName('li');
```

</details>

<details>
<summary>How to select parents, children, descendants, ancestors?</summary>

```JavaScript
const element = document.querySelector('ul');

// parent node (any parent node: element, text etc)
// but in many cases works the same
element.parentNode;
// selects document
document.documentElement.parentNode;
// parent html element
element.parentElement;
// returns null
element.documentElement.parentElement;
// ancestor
element.closest('selector');

// child nodes (any: element, text etc)
element.childNodes;
// returns HTMLCollection - live collection (only DOM elements)
element.children;

// first or last child node
element.firstChild;
element.lastChild;
// first or last child html element
element.firstElementChild;
element.lastElementChild;

// siblings
element.previousSibling;
element.previousElementSibling;
element.nextSibling;
element.nextElementSibling;
```

</details>

<details>
<summary>How to select some html elements with special properties?</summary>

```JavaScript
// to select the <html>
document.documentElement;
// to select the <body>
document.body;
// to select the <head>
document.head;
```

</details>

<details>
<summary>How do some attribute changes work (changes UI/value)?</summary>

```JavaScript
const input = document.querySelector('input');

// UI changes but value html attribute stays the same
// classes, ids etc do change the html attribute
input.value = 'Some new text';
// UI stays the same but value attribute changes
input.setAttribute('value', 'Other text');
```

</details>

<details>
<summary>How to work with data attributes?</summary>

```JavaScript
// html attribute data-cat-name="Cat" can be accessed
const catName = element.dataset.catName;
```

</details>

<details>
<summary>What are data attributes good for?</summary>

- works great for tooltips

</details>

<details>
<summary>How to insert some text to HTML?</summary>

```JavaScript
const element = document.querySelector('section');
// replaces all the content inside the element
element.textContent = 'Some text';
// increments the content
element.textContent++;
// is the same
element.textContent = element.textContent++;
```

</details>

<details>
<summary>How to insert an element to HTML using an HTML string?</summary>

```JavaScript
const element = document.querySelector('section');
// replaces all the content inside the element
element.innerHTML = '<p>Description</p>';
// add html to a specific position
element.insertAdjacentHTML('beforeend', '<p>Description</p>');
```

</details>

<details>
<summary>How to create an element?</summary>

```JavaScript
const newElement = document.createElement('p');
newElement.textContent = 'Description';
```

</details>

<details>
<summary>How to add / move the element to the DOM?</summary>

```JavaScript
// all these methods remove the element (if existed)
// and move to the new position
// (need to clone not to be removed)
// append new DOM element or node
// any node, several nodes (IE not supported)
// last inside the element
element.append('Some text', newElement);
// first inside the element
element.prepend(newElement);
// before the element (as sibling) (problems with Safari)
element.before(newElement);
// after the element (as sibling) (problems with Safari)
element.after(newElement);
// replace existing DOM element or node with a new one
element.replaceWith(newElement);

// only one element (older methods, have IE support)
// = append();
element.appendChild(newElement);
// = before();
// if referenceNode === null, newElement is inserted
// at the end of the element's child nodes
const newNode = element.insertBefore(newElement, referenceNode);
const newNode1 = element.insertBefore(newElement, null);
// = replaceWith();
const oldNode = element.replaceChild(newElement, oldElement);

// alternative method (supports IE, Safari)
element.insertAdjacentElement('beforeend', newElement);
```

</details>

<details>
<summary>How to clone the DOM Node?</summary>

```JavaScript
// deep? boolean
// better to pass an argument
// (default could be different for some browsers)
const newElement = element.cloneNode(true);
```

</details>

<details>
<summary>How to remove the elements from the DOM?</summary>

```JavaScript
const element = document.querySelector('p');

element.innerHTML = '';
// IE is not supported
element.remove();
// works with IE
element.parentElement.removeChild(element);
```

</details>

<details>
<summary>What happens to the event listeners when the element is removed from the DOM?</summary>

- when the element is deleted (no reference left), all the listeners are also cleaned up - no memory leaks

</details>

<details>
<summary>How to work with styles in JS?</summary>

- `style` to get styles but only the inline styles
```JavaScript
const element = document.querySelector('p');

// for CSS properties in several words camelCase is used in JS
element.style.backgroundColor = 'green';
element.style['backgroundColor'] = 'green';
element.style['background-color'] = 'green';
```
- `window.getComputedStyle` to get all styles applied to the element

</details>

<details>
<summary>How to work with the element coordinates relative to the document?</summary>

- always relative to the start of the document, not the viewport (doesn't change upon scrolling)
```JavaScript
// readonly property
const topPosition = element.offsetTop;
```

</details>

<details>
<summary>How to work with the element inner coordinates?</summary>

- inner coordinates of the element do not include the border
- rounds the value to an integer
- the distance from where the margin area ends and the padding and content begins
```JavaScript
// readonly integer property
const innerTop = element.clientTop;
const innerLeft = element.clientLeft;
```

</details>

<details>
<summary>How to work with the element measurements?</summary>

- height of an element's content (including the content not visible on the screen due to overflow)
```JavaScript
// readonly property
const elementFullHeight = element.scrollHeight;
```

</details>

<details>
<summary>How to get the window width and height with and without scroll?</summary>

- in pixels
```JavaScript
// readonly properties
const viewportWidthWithScroll = window.innerWidth;
const viewportHeightWithScroll = window.innerHeight;

// real available window sizes not including the scroll
const viewportWidth = document.documentElement.clientWidth;
const viewportHeight = document.documentElement.clientHeight;
```

</details>

<details>
<summary>How to scroll the content into the viewport?</summary>

```JavaScript
element.scrollIntoView();
```

</details>

<details>
<summary>How to work with templates?</summary>

- `importNode` (learn more)

</details>

<details>
<summary>Learn more</summary>

- [Introduction to the DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)
- [querySelector on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)
- [querySelectorAll on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)
- [getElementById on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById)
- [getElementsByClassName on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName)
- [getElementsByTagName on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/getElementsByTagName)
- [getElementsByName on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByName)
- [insertAdjacentHTML on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentHTML)
- [append on MDN](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/append)
- [appendChild on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild)
- [prepend on MDN](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/prepend)
- [insertBefore on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/insertBefore)
- [before on MDN](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/before)
- [after on MDN](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/after)
- [insertAdjacentElement on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentElement)
- [replaceWith on MDN](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/replaceWith)
- [replaceChild on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/replaceChild)
- [remove on MDN](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/remove)
- [removeChild on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild)
- [getBoundingClientRect on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect)

</details>

## Events
<details>
<summary>What is the general constructor for the event?</summary>

- made with `Event` constructor

</details>

<details>
<summary>What are the specific event constructors?</summary>

- specific constructors inherited from `Event` (ex `MouseEvent`, `DragEvent`)

</details>

<details>
<summary>To what element can you add the event?</summary>

- can be added to any element (even div)

</details>

<details>
<summary>When are the event listeners removed?</summary>

- event listeners are removed when there is no reference to the element left (either in code or DOM)

</details>

<details>
<summary>How to add the listener (2 ways)?</summary>

- `onclick` attribute or adding via JS `element.onclick = console.log();` overrides previous handler (can't add 2 handlers)
- the best way to add events is `element.addEventListener();`

</details>

<details>
<summary>What is the difference between `change` and `input`?</summary>

- `change` works when `field.value` changed and the user finished to enter the value (moved the handle and released)
- `input` works with every value change

</details>

<details>
<summary>How to implement the scroll event?</summary>

- useful for infinite loading
```JavaScript
let currentElementNumber = 0;

const onScroll = () => {
  // measure the distance between our viewport (top left corner)
  // and the end of the page (not viewport)
  const distanceToBottom = document.body.getBoundingClientRect().bottom;
  const viewportHeight = document.documentElement.clientHeight;

  // compare to the window height + threshold
  // if we have < 100px to the end of the content,
  // append new data
  if (distanceToBottom < viewportHeight + 100) {
    const newElement = document.createElement('div');

    currentElementNumber++;
    newElement.innerHTML = `<p>Add element ${currentElementNumber}</p>`;
    document.body.append(newElement);
  }
};

window.addEventListener('scroll', onScroll);
```

</details>

<details>
<summary>What are the event phases?</summary>

- (1) capturing (out - in) => (2) bubbling (in - out)

</details>

<details>
<summary>In what phase does `addEventListener` register the event by default and how to switch the behavior?</summary>

- `addEventListener` by default registers event in a bubbling phase (when we have a listener on button and it's wrapper, first fires button, second wrapper)
- third parameter of `addEventListener(, , true);` switches to the capturing phase (can add to only one listener in a chain)

</details>

<details>
<summary>How to stop the event phases?</summary>

- to prevent propagation
```JavaScript
evt.stopPropagation();
evt.stopImmediatePropagation();
```

</details>

<details>
<summary>What is the event delegation and what are `target` and `currentTarget`?</summary>

- `event.target` is referred to the actual item triggered the event
- `event.currentTarget` always referred to the element, where the listener is added
- `event.target.closest('li');` can also get the item itself

</details>

<details>
<summary>How to trigger DOM events programmatically?</summary>

```JavaScript
// if triggered like that, the event listener added
// is skipped (won't get executed)
// but triggering click event on submit button will work
form.submit();
// works with added listeners
button.click();
```

</details>

<details>
<summary>What is `this` inside the event handler?</summary>

- with arrow functions as handlers `this === window`
- with regular function as handler `this === evt.currentTarget`

</details>

<details>
<summary>How to implement Drag & Drop?</summary>

1. set attribute to `draggable="true"`
2. listen to `dragstart` event (describe the operation and append some data here)
```JavaScript
elementToDrag.addEventListener('dragstart', evt => {
  evt.dataTransfer.setData('text/plain', id);
  evt.dataTransfer.effectAllowed = 'move';
});
```
3. allow to drop into the droppable area (add `preventDefault()` to `dragenter` and `dragover` events)
```JavaScript
// if in drop area we won't prevent default,
// drop event won't be triggered
containerDroppable.addEventListener('dragenter', evt => {
  // can get the data type
  // but not the actual data
  if (evt.dataTransfer.types[0] === 'text/plain') {
    evt.preventDefault();
    // add some visual effect to indicate
    // it's droppable (on dragenter)
    containerDroppable.parentElement.classList.add('droppable');
  }
});

containerDroppable.addEventListener('dragover', evt => {
  if (evt.dataTransfer.types[0] === 'text/plain') {
    evt.preventDefault();
  }
});
```
4. (optional) listen to `dragleave` event (ex. to update some styles)
```JavaScript
containerDroppable.addEventListener('dragleave', evt => {
  // check if only left the element, not just moved
  // to it's children 
  // (w/o this will be triggered when move over the children elements)
  if (evt.relatedTarget.closest('ul') !== containerDroppable) {
    containerDroppable.parentElement.classList.remove('droppable');
  }
});
```
5. listen to `drop` event and update data and UI
```JavaScript
// to react to the drop event need to add a listener
// to the droppable container
containerDroppable.addEventListener('drop', evt => {
  // can get any data we set in dragstart event
  // (now it's available)
  const id = evt.dataTransfer.getData('text/plain');

  // check if the item is in the list and do nothing
  // if not - add item to the list and remove where it was
});
```
6. (optional) listen to `dragend` event and update data and UI (triggered event when the drag was canceled)
```JavaScript
// is added to a draggable element
elementToDrag.addEventListener('dragend', evt => {
  // check if the drag wasn't done
  evt.dataTransfer.dropEffect === 'none';
});
```

</details>

<details>
<summary>Learn more</summary>

- [ ] [Introduction to events on MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)
- [ ] [Event reference on MDN](https://developer.mozilla.org/en-US/docs/Web/Events)
- [ ] [Event on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Event)
- [ ] [Drag and drop API on MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API)

</details>

## Timers and intervals

## Async JavaScript (promises and callbacks, async/await), http requests
<details>
<summary>What is sync data loading?</summary>

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

<details>
<summary>What is the event loop and how it works?</summary>

- JS is single threaded
- browser is multi threaded
- all kind of async tasks (like timers, event listeners, etc) are going to browser (message queue)
- micro - promises (run first), macro - timeouts (run second)
- when the call stack is empty, event loop goes through message queue and executes the functions from there

</details>

<details>
<summary>What is async?</summary>

- async - run the operation without blocking the main script process

</details>
  
<details>
<summary>How was async implemented in ES5 and what are the issues?</summary>

- complex interface, have to add all possible callbacks, difficult to make optional manipulation for some cases
- difficult to read the code, recreate the methods sequence is quite hard
- callback hell - several chained async methods turn into nested sequences of callbacks, too hard to support https://callbackhell.ru/
```JavaScript
const getResponse = (url, onload, onerror) => {
  const xhr = new XMLHttpRequest();
  xhr.open('GET', url, true);
  xhr.onload = () => onload(xhr.response);
  xhr.onerror = () => onerror(xhr.status);
  xhr.send();
};

getResponse('data.json',
  (response) => console.log(response),
  (errorStatus) => console.log(errorStatus)
);
```

</details>

<details>
<summary>How is async implemented in ES6?</summary>

- promise is a way to work with an async function as if it's sync 
- different states of a promise object
<img src="../images/promise.jpg" alt="promises" width="400">

```JavaScript
const getResponse = (url) => new Promise(
  (resolve, reject) => {
    // Object => Pending...
    // neither then() or catch() executes at this moment
    const xhr = new XMLHttpRequest();
    xhr.open('GET', url);
    // Object => Fulfilled
    // then() executes
    xhr.onload = () => resolve(xhr.response);
    // Object => Rejected
    // catch() executes
    xhr.onerror = () => reject(xhr.status);
    xhr.send();
  }
);

getResponse('data.json')
  // callback on success
  // could work with several promises
  // returns new Promise()
  .then(
    (data) => console.log(data),
    // but better to use catch
    (error) => console.warning(error)
  );

getResponse('data.json')
  // if there is anywhere in then chain throw new Error
  // it's going to be caught in catch
  .then((data) => console.log(data))
  // catches all the errors before
  // the blocks before are skipped but
  // doesn't stop the chain (if there are some then after)
  .catch((error) => console.warning(error))
  // if there are no more then() blocks left
  // promise enters the final mode: settled
  // once settled, you can use the special block finally()
  // to do some cleanup work
  // this block is reached anyways (resolve or reject before)
  // optional, executes always
  // will not return a promise in the end (like then() and catch())
  .finally(cb);

// you can work with promises chaining then
// every then returns a promise, where we can also call then
Promise.resolve('a') // 'a'
  .then((val) => val.concat('b')) // 'ab'
  // when we have another then() or catch()
  // the promise re-enters pending mode
  .then((val) => val.concat('c')) // 'abc'
  .then((val) => val.concat('d')); // 'abcd'
```

</details>

<details>
<summary>What is Promise.race?</summary>

```JavaScript
Promise.race([getPromise1(), getPromise2()])
  .then(dataFromTheFastest => {});
// the other promise is not canceled!
// just ignored (the http request will still be sent)
```

</details>

<details>
<summary>What is the difference between Promise.all and Promise.allSettled?</summary>

- when you need an array of requests at the same time 
  - `Promise.all(<Array.Promise>)`
    - executed when all the promises are resolved
    - if one with error, drops, can't access the data
    - returns an array
  - `Promise.allSettled(<Array.Promise>)`
    - waits till all the promises are completed (success/error)
    - can access the data even when some promises complete with an error
    - poor browser support
- `Promise.then` could return
  - just value/array - goes to the next promise
  - object Promise
  - array of values / promises - can turn into something else

</details>

<details>
<summary>What is async await?</summary>

- uses promises under the hood
- can be used only with functions
```JavaScript
// can't use like that
await setTimer(1000);
// but can wrap into IIFE
(async function() {
  await setTimer(1000);
})();
```
- when `async` is added, function automatically returns a promise
- wraps everything inside into a promise
```JavaScript
const setTimer = async () => {
  // waits till the promise is resolved and goes to the next line
  const data = await getData();
  const otherData = await getOtherData();
  // won't get executed till the await block resolved
  // as if wrapping into then() block
  console.log('Done!');
  // returns promise
};

async function setTimer() {
  // to handle errors can use try ... catch
  try {
    // if anything here yields an error,
    // the block fails into the catch
    // if error is in the 1st line, 2nd won't be executed
    const data = await getData();
    const otherData = await getOtherData();
  } catch (error) {
    console.log(error);
  }
  // this code will be executed anyways
  console.log('Done!');
  // returns promise
}

// creates a wrapping promise
function setTimer() {
  return new Promise((resolve, reject) => {
    // all the code here
  });
}
```
- `await` wraps everything into a `then()` block
- not good for cases when we need to run some code and not wait for promise to resolve or reject

</details>

<details>
<summary>What is Http?</summary>

- Data transfer protocol - the way computer uses to exchange the information (there are many different protocols, in the web we use http)
- HTTP - hypertext transfer protocol - client exchanges data with the server
- HTTP request is always text
- request to the server = text
```
GET /index.html HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
Accept: text/html
```
- server response = text
```
HTTP/1.1 200 OK
Cache-Control: max-age=604800
Content-Type: text/html
Date: Tue, 24 Oct 2017 11:08:24 GMT
Etag: "359670651+ident"
Expires: Tue, 30 Oct 2017 11:08:24 GMT
Last-Modified: Fri, 09 Aug 2016 23:23:35 GMT
Server: ECS (dcs/53DB)
Vary: Accept-Encoding
X-Cache: HIT
Content-Length: 1270

<!doctype html>
<html>
  <head></head>
  <body></body>
</html>
```

</details>

<details>
<summary>How to send the http request with XMLHttpRequest?</summary>

```JavaScript
// can be used on its own
const xhr = new XMLHttpRequest();
xhr.open('GET', 'https://google.com');
xhr.send();

// or inside a function
const sendRequest = (method, url) => {
  const xhr = new XMLHttpRequest();

  xhr.open(method, url);
  xhr.responseType = 'json';
  // to add more headers use the method multiple times
  xhr.setRequestHeader('Content-Type', 'application/json');
  
  // to get and use the data have to listen to onload event
  // for XHR .addEventListener is not supported in some browsers
  xhr.onload = function() {
    // check if the status is success
    if (xhr.status >= 200 && xhr.status < 300) {
      // JSON data (mostly, depends on server)
      console.log(xhr.response);
      // either parse JSON.parse(...)
      // or configure responseType (will be parsed automatically)
    } else {
      console.log(xhr.response);
      console.log('Something went wrong.');
    }
  };
  
  // not for sent requests (when we get a response)
  // only for the errors of sending the request
  // like timeout or wasn't sent
  xhr.onerror = function() {
    console.log(xhr.response);
    console.log(xhr.status);
  };
  
  xhr.send();
};

// with using a promise
const sendHttpRequest = (method, url, data) => {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();

    xhr.setRequestHeader('Content-Type', 'application/json');
    xhr.open(method, url);
    xhr.responseType = 'json';

    xhr.onload = function() {
      if (xhr.status >= 200 && xhr.status < 300) {
        resolve(xhr.response);
      } else {
        reject(new Error('Something went wrong!'));
      }
    };

    xhr.onerror = function() {
      reject(new Error('Error while sending a request!'));
    };

    xhr.send(JSON.stringify(data));
  });
};

const fetchPosts = () => {
  sendHttpRequest('GET', 'https://...')
    .then(responseData => console.log(responseData))
    .catch(error => console.log(error));
};

const addPosts = async () => {
  try {
    const responseData = await sendHttpRequest(
      'POST',
      'https://...',
      post
    );
  } catch (error) {
    console.log(error);
  } 
};
```

</details>

<details>
<summary>How to use fetch API?</summary>

- `fetch` is a wrapper around promise
- function for sending/fetching data (`XMLHttpRequest` under hood)
```JavaScript
// response.json(); returns promise
// resolves when the string will parse json into an object
// if no 2nd param, get request, returns Promise
// resolves into response object
// if fetch => error, but the response is received,
// fetch doesn't count it as a throw new Error (for catching inside catch)
// and returns that response into then
// because the request is fulfilled and response received from server
// 404 / redirect / etc - for fetch those are normal server responses
// so have to add our own status handling
fetch('https://data.com', {
  method: 'POST',
  body: JSON.stringify({
    'date': Date.now(),
    'time': 402,
    'lives': 3
  }),
  headers: {
    'Content-Type': 'application/json'
  }
});

const sendHttpRequest = (method, url, data) => {
  // returns a JSON (unparsed), have to parse
  // with .json() available in fetch API
  return fetch(url, {
    method: method,
    body: JSON.stringify(data)
  })
    .then(response => {
      if (response.status >= 200 && response.status < 300) {
        return response.json();
      } else {
        // if we need the response, error handling could be tricky
        return response.json()
          .then(errorData => {
            console.log(errorData);
            throw new Error('Something went wrong on the server side!');
          });
      }
    })
    .catch(error => {
      console.log(error);
      throw new Error('Something went wrong with the request!');
    });
};
```

</details>

<details>
<summary>What are the good parts for feedback in the UI?</summary>

- When you sync data with a server, don't change control state, change only if the request was successful (returned 200+ codes)
- View => Model => Server => Model => View
- click on favorites - gone on update, if there was an error response from server
- comment doubles if you don't disable the submit button

</details>

<details>
<summary>Learn more</summary>

- [ ] [JavaScript Promises: An introduction](https://web.dev/promises/)
- [ ] [async function on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
- [ ] [HTTP request methods on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- [ ] [HTTP Messages on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages)
- [ ] [HTTP response status codes on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [ ] [HTTP Headers on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
- [ ] [Using XMLHttpRequest on MDN](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest)
- [ ] [Fetch API on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- [ ] [Using files from web applications on MDN](https://developer.mozilla.org/en-US/docs/Web/API/File/Using_files_from_web_applications)

</details>

## Forms
<details>
<summary>What is the basic implementation of show password case?</summary>

- change type of input from `password` to `text`

</details>

<details>
<summary>Learn more</summary>

- [How to Build and Validate Beautiful Forms with Vanilla HTML, CSS, & JS](https://www.freecodecamp.org/news/build-and-validate-beautiful-forms-with-vanilla-html-css-js/)

</details>

## Authorization
<details>
<summary>What is the purpose of the authorization?</summary>

- restricts the access for different users

</details>

<details>
<summary>What are the ways to identify the user?</summary>

- Identification - tell the site who you are
- Authentication - (authentic - true, genuine) the confirmation that you are who you state you are
- Authorization - check if you are allowed to get access to some parts of the website or webapp

</details>

<details>
<summary>What is the authorization order?</summary>

1. Identification - user enters login and password
2. Authentication - server checks if the login and password are correct and gives a token (access to the web app, often holds the rules and never stores open)
3. Authorization - you give the token to the server and the server decides whether to give you an access or not
  - 200 - success, allowed
  - 401 - unauthorized
  - 403 - not enough rights

</details>

## Working with data
<details>
<summary>What are the main problems when working with data?</summary>

- user input - user can enter unsafe data for the view and UI has to be ready for it
- storing and passing data formats could be different to the format needed on the UI, so we need to convert data in our app
  - some ES6 objects (Date, Sets, Maps) could not be converted to JSON, so have to convert into standard data types (primitives, arrays, objects)

</details>

<details>
<summary>What is JSON (and the restrictions)?</summary>

- JavaScript Object Notation
- can't use functions here
- for keys only `" "`
- for values `"string"` (double quotes only), `10`, `true`, `{...}`, `[...]`, `null`

</details>

<details>
<summary>How to get the parameters from the link?</summary>

```JavaScript
const url = new Url(location.href);
const queryParams = url.searchParams;
const data = queryParams.get('data');
```

</details>

<details>
<summary>How to convert into a link?</summary>

- `encodeURI('some text');`

</details>

<details>
<summary>Learn more</summary>

- [ ] [Why Mutation Can Be Scary](https://alistapart.com/article/why-mutation-can-be-scary/)

</details>

## Loading scripts to the page
<details>
<summary>How to load script files from JS dynamically?</summary>

- basically generate html and add it to the page

</details>

## Location API
<details>
<summary>What is the location API used for?</summary>

- for the app url and navigation

</details>

<details>
<summary>Learn more</summary>

- [ ] [Location on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Location)

</details>

## History API
<details>
<summary>What is history API used for?</summary>

- works with location
- can use `history.back()` to navigate back (ex different cases with questions like age)

</details>

## Navigator API
<details>
<summary>Why do we use the navigator API?</summary>

- don't use for defining browser version
- could be useful when we need
  - geolocation

</details>

<details>
<summary>Learn more</summary>

- [ ] [Navigator on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Navigator)

</details>

## Browser storage
<details>
<summary>What are local and session storages and what is the difference?</summary>

- simple key-value store
- local storage lives till either user or browser (when ran out of space) clears it
- session storage lives in the browser while you don't close the tab

</details>

<details>
<summary>What are local and session storages good for?</summary>

- manage user preferences or basic user data
- simple, easy to use, but bad for complex data

</details>

<details>
<summary>How are local and session storages being cleared?</summary>

- can be cleared by the user and via JS

</details>

<details>
<summary>How to work with the local storage?</summary>

```JavaScript
// local storage works sync
const userId = '775';
const user = {
  name: 'Harry',
  age: 33
};

// JS converts data into a string
localStorage.setItem('userId', userId);
localStorage.setItem('user', user); // => [object Object]
localStorage.setItem('user', JSON.stringify(user));

// to get item
localStorage.getItem('user');
```

</details>

<details>
<summary>How to work with the session storage?</summary>

```JavaScript
// session storage works sync

// JS converts data into a string
sessionStorage.setItem('userId', userId);
sessionStorage.setItem('user', JSON.stringify(user));

// to get item
sessionStorage.getItem('user');
```

</details>

<details>
<summary>What are cookies and the difference from local/session storage?</summary>

- cookie stored to server
- simple key-value store with some config options
- not as easy to use
- the advantage is that you can set it to expire or send to a server
- available only if your app is served on a running server

</details>

<details>
<summary>What are cookies good for?</summary>

- manage user preferences or basic user data
- bad for complex data

</details>

<details>
<summary>How to clear the cookies?</summary>

- can be cleared by the user and via JS

</details>

<details>
<summary>How to use cookies?</summary>

```JavaScript
// cookies work sync
const userId = 'fd3928';
const user = {
  name: 'Harry',
  age: 33
};
// data stored as a string
// under the hood uses a setter
// so adds new cookie, not overrides
document.cookie = `userId=${userId}; max-age=360`; // => seconds
document.cookie = `user=${JSON.stringify(user)}; expires=date`; // => date

// to get info
// returns all the cookies stored in one string
document.cookie;
```

</details>

<details>
<summary>What is IndexedDB?</summary>

- client-side database

</details>

<details>
<summary>What is IndexedDB good for?</summary>

- manage complex data your app needs
- not as easy to use, great for complex (non-critical) data, good performance (good for usage like google sheets)

</details>

<details>
<summary>How to clean the IndexedDB?</summary>

- can be cleared by the user and via JS

</details>

<details>
<summary>How to use IndexedDB?</summary>

```JavaScript
// indexedDB works sync
// 1. open a database
// pass name and version
// creates or opens an existed DB
const dbRequest = indexedDB.open('Name', 1);
let db;

// to be able to change the data from a button too
dbRequest.onsuccess = function(evt) {
  // access to the created database
  db = evt.target.result;
};

// for better browser support not .addEventListener, but:
// this event runs when the db is created or the version is upgraded
dbRequest.onupgradeneeded = function(evt) {
  db = evt.target.result;

  // 2. create an object store
  const objStore = db.createObjectStore('products', {keyPath: 'id'});

  // 3. start a transaction and make a request to do some db operation
  // 4. wait for the operation to complete
  // 5. do something with the results
  // oncomplete triggers when createObjectStore is finished
  objStore.transaction.oncomplete = function(evt) {
    // connecting to the data base
    // name of the store + mode (readonly, readwrite, etc)
    const productsStore = db.transaction('products', 'readwrite')
      .objectStore('products');
    // adding a new item, has to have the property from keyPath
    productsStore.add({
      id: 'pr1',
      name: 'Product 1',
      price: 1.22,
      tags: ['Vegetarian', 'No-Sugar']
    });
  };
};

dbRequest.onerror = function() {};

addButton.addEventListener('click', () => {
  if (!db) {
    return;
  }

  const productsStore = db.transaction('products', 'readwrite')
    .objectStore('products');

  productsStore.add({
    id: 'pr2',
    name: 'Product 2',
    price: 1.42,
    tags: ['Vegetarian', 'No-Sugar']
  });
});

// to retrieve the data
getButton.addEventListener('click', () => {
  const productsStore = db.transaction('products', 'readwrite')
    .objectStore('products');

  const request = productsStore.get('pr1');

  request.onsuccess = function() {
    console.log(request.result);
  };
});
```

</details>

<details>
<summary>Learn more</summary>

- [ ] [localStorage on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)
- [ ] [cookie on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie)
- [ ] [Using IndexedDB on MDN](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Using_IndexedDB)

</details>

## Service Workers, Web Workers and Worklets
<details>
<summary>Learn more</summary>

- [ ] [Web workers vs Service workers vs Worklets](https://bitsofco.de/web-workers-vs-service-workers-vs-worklets/)

</details>

## Meta-programming
<details>
<summary>When do you need to use meta-programming?</summary>

- advanced concepts used mostly when you create libraries

</details>

<details>
<summary>What are Symbols and how to use them?</summary>

- primitive values
- used as keys in objects
- built-in symbols and creatable symbols
- uniqueness is guaranteed
```JavaScript
const userId = Symbol(); // => Symbol()
const playerId = Symbol('id'); // => Symbol(id)

const player = {
  [playerId]: 1, // can't access this property out of library
  name: 'Harry',
  level: 11
};

// can use inside the library
player[playerId] = 2;

console.log(playerId === Symbol('id')); // => false

// built-in symbol
const user = {
  name: 'Ron',
  level: 9,
  [Symbol.toStringTag]: 'User'
};

console.log(user.toString()); // => [object User]
```

</details>

<details>
<summary>What are Iterators and how to use them?</summary>

- create your own iterable values
- iterables use it internally
- iterator is an object which has `next()` method
```JavaScript
const player = {
  currentFriend: 0,
  name: 'Harry',
  friends: ['Ron', 'Hermione', 'Luna'],
  next() {
    if (this.currentFriend >= this.friends.length) {
      return {value: this.currentFriend, done: true};
    }

    const result = {
      value: this.friends[this.currentFriend],
      done: false
    };

    this.currentFriend++;
    return result;
  }
};

console.log(player.next());
console.log(player.next());
console.log(player.next());
console.log(player.next());

// still can't use for loop, but while is ok
let friend = player.next();

while(!friend.done) {
  console.log(friend.value);
  friend = player.next();
}
```

</details>

<details>
<summary>What are Generators and how to use them?</summary>

- using generators to build an iterator object
- generator is special function which generates an iterator
- returns an object with `next()` method
```JavaScript
const player = {
  name: 'Harry',
  friends: ['Ron', 'Hermione', 'Luna'],
  // value should be an iterator
  // returns an object with next() method
  [Symbol.iterator]: function* friendGenerator() {
    // we can have both, generator and separate next() method
    let currentFriend = 0;

    while(currentFriend < this.friends.length) {
      // almost like return
      // pauses the execution on first call
      // and continues on second and so on
      // that's why we get different values
      yield this.friends[currentFriend];
      currentFriend++;
    }
  }
};

// now we can use loops
// for loop and some other (like spread)
// look for the [Symbol.iterator] function
// so all iterables have it by default
for (let friend of player) {
  console.log(friend);
}

console.log([...player]);

// if instead of [Symbol.iterator] different name is used
// can use it like that
// in this case value is the same (we generate new generator)
console.log(player.getFriend().next());
console.log(player.getFriend().next());
console.log(player.getFriend().next());

// but if we store it, the value will be different
const friendsIterator = player.getFriend();

console.log(friendsIterator.next());
console.log(friendsIterator.next());
console.log(friendsIterator.next());
```

</details>

<details>
<summary>What is Reflect API and how to use it?</summary>

- API to control objects
- standardized and grouped methods
- control code usage/impact
- has the same methods and properties as `Object`, but `Reflect` is new and has more methods
  - better error handling (`Object` sometimes returns undefined or just fails silently)
  - all the methods are present (`Object` doesn't have delete property method, have to use `delete obj.prop;`)
- gives a handful of methods to change object on a meta level
```JavaScript
const player = {
  name: 'Harry Potter'
};

Reflect.setPrototypeOf(player, {
  toString() {
    return this.name;
  }
});
```

</details>

<details>
<summary>What is Proxy API and how to use it?</summary>

- create traps for object operations
- step in and execute code
- control code usage/impact
```JavaScript
const player = {
  name: 'Harry Potter'
};

const playerHandler = {
  // executes when somebody tries to read a value
  // arguments are passed automatically by Proxy API
  get(obj, propertyName) {
    console.log(propertyName);
    return obj[propertyName] || 'NOT FOUND';
  },

  // executes when we try to set a value
  set(obj, propertyName, newValue) {
    if (propertyName === 'age') {
      return;
    }

    obj[propertyName] = newValue;
  }
};

// new Proxy(object, handlers)
const proxyPlayer = new Proxy(player, playerHandler);

console.log(proxyPlayer.name);
// => name
// => Harry Potter
console.log(proxyPlayer.age); // => NOT FOUND
proxyPlayer.age = 10;
// because of the set trap
console.log(proxyPlayer.age); // => NOT FOUND
```

</details>

<details>
<summary>Learn more</summary>

- [ ] [Symbol on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)
- [ ] [Iterators and Generators on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators)
- [ ] [Reflect API on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect)
- [ ] [Proxy API on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy)

</details>

## Performance and optimizations
<details>
<summary>How does the code parse, compiles, executes?</summary>

<img src="../images/code-parsing.png" alt="Code parsing">

<img src="../images/heap-stack.png" alt="Heap, stack (how JS engine works)">

- JS is single-threaded
- event loop is not a JS-engine feature (only heap and stack - simple sync code), it's a browser feature

</details>

<details>
<summary>What are Primitive and Reference values?</summary>

- primitive - strings, numbers, booleans, `null`, `undefined`, symbol
  - stored in a memory (normally on stack)
  - variable stores the value itself
  - copying a variable copies the value
- reference - all other objects (more expensive to create)
  - stored in a memory (heap)
  - variable stores a pointer (address) to location in memory
  - copying a variable copies the pointer (reference)

</details>

<details>
<summary>How do the Garbage collection and Memory management work?</summary>

- the stack is cleared automatically (mostly ok)
- the heap may overflow more frequently
  - if exceeded the allocated memory for the browser (chrome crashes the site, but the app still runs)
  - no need to manually manage in most cases
- V8 garbage collector
  - periodically checks the heap for unused objects (objects without references) and removes them
- memory leaks (due to unused objects you still hold the reference to)
```JavaScript
function printMsg() { ... }

function addListener() {
  // JS replaces the function, the listener is only one
  button.addEventListener('click', printMsg);

  // JS adds the new listener every time
  button.addEventListener('click', function() { ... });
}
```

</details>

<details>
<summary>Learn more</summary>

- [Reference vs Primitive values](https://academind.com/learn/javascript/reference-vs-primitive-values/)
- [Memory Management](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management)
- [JavaScript V8 Engine Explained](https://hackernoon.com/javascript-v8-engine-explained-3f940148d4ef)
- [Getting garbage collection for free](https://v8.dev/blog/free-garbage-collection)

</details>

## Security
<details>
<summary>What are the Potential Security Holes?</summary>

- security details in the code (like connection strings, keys, user data)
- keep in mind that JS code could be read by everyone
- security relevant details can be read
- ex: database access credentials exposed in code (not the issue with google API Key, can restrict that)

</details>

<details>
<summary>What are the XSS Attacks?</summary>

- attack pattern when malicious JS code gets injected and executed
- injected code can do anything your code could do as well
- vary dangerous, gives full control for hackers
- ex: unchecked user-generated content
```HTML
<!-- new versions of browsers don't execute -->
<script>alert('Hello!');</script>
<!-- always runs -->
<img src="" onerror="alert('Hello!');">
```
- use `textContent` instead of `innerHTML` if possible
- use packages like `sanitize-html`, also validate on server side
- use the third party libraries you trust

</details>

<details>
<summary>What is the Cross-Site Request Forgery (CSRF)?</summary>

- attack pattern that depends on injected content (ex: images)
- requests to malicious servers are made with user's cookies
- actions can be executed without the user knowing
- ex: malicious image URL, XSS
- mostly backend security issue (CSRF token to deal with the issue)
<img with="500" src="./images/csrf.png">

</details>

<details>
<summary>What is the Cross-Origin Resource Sharing (CORS)?</summary>

- not an attack pattern but a security concept
- requests are only allowed from the same origin (domain)
- controlled via server-side response headers and browser
- ex: JS modules (that's why we need to run a server - are only allowed if modules are from the same server)

</details>

## Regular expressions
<details>
<summary>Some common cases</summary>

- `myRegEx.test(myString);` to check if any part of the string matches
- `myString.match(myRegEx);` to check if there is this part in a string and extract it (returns `['matching part']`)
- case matters `/Kevin/` !== `/kevin/`
- add `i` flag to ignore the case `/kevin/i`
- add `g` flag to search or extract a pattern more than once `/little/g`, match returns `['match', 'match']` or more items
- to alternate search use `|` `/yes|no/`
- if you wanted to match "hug", "huh", "hut", and "hum", you can use the regex `/hu./` to match all four words (wildcard `.` matches any one character)
- `/[abc]/` character classes to define a group of characters you wish to match, ex "bag", "big", and "bug" but not "bog" `/b[aiu]g/`
- `/[a-e]/` works the same as character classes but given a group of characters to match
- `/[0-9]/` for numbers
- `/[a-e0-9]/` for numbers and letters
- `/[^aeiou]/gi` to create a negated character set, you place a caret character after the opening bracket and before the characters you do not want to match
- `+` the character or pattern has to be present consecutively (the character has to repeat one after the other) `/a+/g` will match 
  - `['a']` - `"abc"`
  - `['aa']` - `"aabc"`
  - `['a', 'a']` - `"abab"`
- `*` for 0 or more occurrence `/go*/`
- `/t[a-z]*i/` is greedy and matches the largest substring, ex `titanic` => `['titani']`
- `/t[a-z]*?i/` lazy matching `titanic` => `['ti']`
- `/^a/` matches the beginning of a string
- `/a$/` matches the ending of a string
- `/\w/` === `/[A-Za-z0-9_]/`
- `/\W/` the opposite to `/\w/`
- `/\d/` for numbers and `/\D/` is an opposite
- `/\s/` not only matches whitespace, but also carriage return, tab, form feed, and new line characters === character class `/[ \r\t\f\n\v]/` `/\S/` is an opposite
- `/a{3,5}h/` to match only the letter a appearing between 3 and 5 times in the string "ah"
- `/ha{3,}h/` to specify only the lower count
- `/ha{3}h/` exact number of matches
- `/u?/` checks for zero or one of the preceding element, you can think of this symbol as saying the previous element is optional
- `/q(?=u)/` => `['q']` positive lookahead will look to make sure the element in the search pattern is there, but won't actually match it
- `/q(?!u)/` => `['q']` negative lookahead will look to make sure the element is not there, won't match it
- `/(a|b)/` are used to group patterns
- () are used to find repeat substrings
- `/(\w+)\s\1/` matches any word that occurs twice separated by a space, `.match()` method on a string will return an array with the string it matches, along with its capture group

</details>

<details>
<summary>Learn more</summary>

- [8 полезных регэкспов с наглядным разбором](https://habr.com/ru/post/66931/)
- [Regex testing service](https://regex101.com/)
- [A collection of different regexps](http://html5pattern.com/)
- Mastering Regular Expressions (O'Reilly, by Jeffrey Friedl)

</details>

## Deploying

## Testing

## Debugging
<details>
<summary>What are the common console methods?</summary>

```JavaScript
console.log();
console.debug();
console.error();
console.info();
console.warn();
```

</details>

<details>
<summary>How to console log as an object instead of the html tree?</summary>

- if by default logs the html tree, use to log as an object
```JavaScript
console.dir(document);
```

</details>

<details>
<summary>How to console log as a table?</summary>

- for nice table overview
```JavaScript
console.table([1, 2, 3]);
```

</details>

<details>
<summary>How to clear the console?</summary>

```JavaScript
console.clear();
```

</details>

<details>
<summary>Learn more</summary>

- [Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/)
- [Get Started with Debugging JavaScript in Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/javascript/)
- [A Guide to Console Commands](https://css-tricks.com/a-guide-to-console-commands/)

</details>

## Browser support
<details>
<summary>Feature detection and fallbacks</summary>

```JavaScript
// if not supported === undefined
if (navigator.clipboard) {
  navigator.clipboard.writeText('Some text to copy.')
    .then(result => console.log(result))
    .catch(error => console.log(error));
} else {
  console.log('Feature is not available, try to copy manually.');
}
```

</details>

<details>
<summary>Transpiling the code</summary>

- something like babel could be integrated into webpack config `modules`
- set browsers list in `package.json`

</details>

<details>
<summary>Polyfills</summary>

- can add manually
- and also with babel it's available to add an auto detection

</details>

<details>
<summary>If JavaScript is off in the browser</summary>

- at least use `<noscript>Please turn on the JavaScript support.</noscript>` 

</details>

<details>
<summary>Learn more</summary>

- [ ] [What is Babel?](https://babeljs.io/docs/en/)
- [ ] [Babel loader](https://github.com/babel/babel-loader)
- [ ] [@babel/preset-env](https://babeljs.io/docs/en/babel-preset-env)
- [ ] [core-js](https://github.com/zloirock/core-js)

</details>

## Tools and workflow
<details>
<summary>Learn more</summary>

- [Introduction to JavaScript Source Maps](https://www.html5rocks.com/en/tutorials/developertools/sourcemaps/)

</details>

## Libraries
<details>
<summary>Working with dates</summary>

- [Flatpickr](https://flatpickr.js.org/getting-started/)
- [Moment.js](https://momentjs.com/)

</details>

<details>
<summary>Animations</summary>

- [Mojs](https://mojs.github.io/)

</details>

<details>
<summary>Charts</summary>

- [Chart.js](https://www.chartjs.org/)

</details>

<details>
<summary>Security</summary>

- [He.js](https://github.com/mathiasbynens/he)

</details>

<details>
<summary>Maps</summary>

- [OpenLayers](https://openlayers.org/en/latest/doc/quickstart.html)

</details>

## Frameworks

- [ ] [Angular vs React vs Vue](https://academind.com/learn/angular/angular-vs-react-vs-vue-my-thoughts/)

## Resources
<details>
<summary>Read</summary>

- [JavaScript Garden](http://shamansir.github.io/JavaScript-Garden/)

</details>

<details>
<summary>Practice</summary>

- [JavaScript Questions](https://github.com/lydiahallie/javascript-questions)
- [Codewars](https://www.codewars.com/dashboard)
- [FreeCodeCamp](https://www.freecodecamp.org/)
- [HackerRank](https://www.hackerrank.com/dashboard)
- [CodinGame](https://www.codingame.com/)

</details>

<details>
<summary>Create</summary>

- [Responsive and Dynamic Progress Bar with HTML, CSS, and JavaScript](https://www.freecodecamp.org/news/how-to-build-a-responsive-and-dynamic-progress-bar/)

</details>

<details>
<summary>Courses</summary>



</details>

<details>
<summary>Books</summary>

- [You Don't Know JS](https://github.com/getify/You-Dont-Know-JS) by Kyle Simpson
- [Head First JavaScript Programming (O'Reilly, by Elisabeth Robson, Eric Freeman)
- [JavaScript: The Definitive Guide (O'Reilly, by David Flanagan)
- [JavaScript: The Good Parts (O'Reilly, by Douglas Crockford)
- [JavaScript Patterns (O'Reilly, by Stoyan Stefanov)

</details>