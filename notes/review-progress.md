# Review progress and questions I have to review
## 03, ..., 27 Nov 2020 (04 Dec)
### JavaScript

<details>
<summary>What is the type of null?</summary>

```JavaScript
// 2 - null
console.log(typeof null); // => object
```

</details>

<details>
<summary>What system JS uses to work with numbers?</summary>

- JS works with binary numbers and converts into decimal

</details>

<details>
<summary>How does BigInt work and when do we use it?</summary>

- only integer, decimal => error
```JavaScript
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
<summary>How to check if a string contains some text?</summary>

```JavaScript
const playerName = 'Harry Potter';

// case sensitive
console.log(playerName.includes('rr')); // => true
console.log(playerName.includes('h')); // => false
```

</details>

<details>
<summary>What is an iterable (and examples)?</summary>

- objects that implement the 'iterable' protocol (have an `@@iterator` method (ex: `Symbol.iterator`))
- basically objects where you can use `for ... of` loop
- Array, NodeList, String, Map, Set, etc.

</details>

<details>
<summary>How to create an array?</summary>

```JavaScript
// before ES6
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

## 05, ..., 27 Nov 2020 (04 Dec)
### JavaScript
<details>
<summary>How are the numbers stored?</summary>

- every number is a float
- numbers are stored as 64 Bit Floating Points (some issues and limits)

</details>

<details>
<summary>What are the maximum and minimum numbers?</summary>

```JavaScript
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
<summary>How to delete or add an element from (to) an array at the start or the end?</summary>

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
<summary>How to delete or add an element from (to) an array at any position?</summary>

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

## 06, ..., 27 Nov 2020 (03, 10 Dec)
### JavaScript
<details>
<summary>How to make an array of a string?</summary>

```JavaScript
const text = 'One two three';
const words = text.split(' '); // => ['One', 'two', 'three']
const words2 = Array.from(text); // => ['O', ..., ' ', 't', ...]
```

</details>

<details>
<summary>How to copy an array or a part of it?</summary>

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
<summary>How to find an item or an index in an array?</summary>

```JavaScript
const numbers = [1, 2, 5];
// first element in the array
const number = numbers.find(number => number > 1); // => 2
// index of the first element or -1
const numberIndex = numbers.findIndex(number => number > 1); // => 1
```

</details>

<details>
<summary>How and why to create a stack using an array (LIFO)?</summary>

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
<summary>How and why to create a queue using an array (FIFO)?</summary>

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

## 08, ..., 27 Nov 2020 (03, 10 Dec)
### JavaScript
<details>
<summary>How to create the set and add items?</summary>

```JavaScript
const data = new Set();
// add items
data.add(1);

// based on array or any other iterable
const data = new Set([1, 4, 8]);
```

</details>

<details>
<summary>How to check if the item is in the set?</summary>

```JavaScript
const isElementInData = data2.has(1); // => true
```

</details>

<details>
<summary>How to delete the item and what if there is no such item?</summary>

```JavaScript
const data = new Set([1, 4, 8]);
// delete not existed item does nothing
data.delete(1);
```

</details>

<details>
<summary>Is set an iterable and how to iterate?</summary>

```JavaScript
const data = new Set([1, 4, 8]);
// iterable
for (const item of data) {
  console.log(item);
}
```

</details>

<details>
<summary>What are the entries of the set?</summary>

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

## 10, ..., 27 Nov 2020 (02, 08, 15 Dec)
### JavaScript
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

## 12, ..., 28 Nov 2020 (02, 07, 13, 20 Dec)
### JavaScript
<details>
<summary>What data structures could be used as a key in an Object?</summary>

- strings
- numbers (positive int or floats)
- symbols

</details>

<details>
<summary>How to create an Object?</summary>

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
<summary>How the keys are ordered when logging?</summary>

```JavaScript
const person = {
  'short-name': 'Ron',
  age: 22,
  level: 3,
  3.2: 'some value',
  walk: function() {}
};

// collapsed = the object (if not all the keys are numbers) is not sorted
// if numbers = order ascending
// when not collapsed = any object is sorted, numbers first
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

## 13, ..., 28 Nov 2020 (02, 07, 13, 20 Dec)
### JavaScript
<details>
<summary>How to iterate (entries, values, keys)?</summary>

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
<summary>How to check if the property exists?</summary>

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
<summary>What does function without `return` statement return?</summary>

- function without `return` statement returns `undefined`

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
<summary>What are the default parameters and how to use them?</summary>

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
<summary>What is the arguments keyword?</summary>

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

## 16, ..., 27 Nov 2020 (30, 04, 09, 15, 22 Dec)
### JavaScript
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

## 17, ..., 28 Nov 2020 (01, 05, 10, 16, 23 Dec)
### JavaScript
<details>
<summary>What is a scope and a context?</summary>

- scope is where the function runs
- context depends on how the function is called
- while the function is not called, it doesn't have any context
- context is being created upon the function call

</details>

## 24, ..., 29 Nov 2020 (01, 04, 06, 13, 19, 26 Dec)
### JavaScript
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

- in an object (method) `this` is the link to the object itself (but remember, in depends on how the function is called)

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

## 26, ..., 29 Nov 2020 (01, 03, 06, 08, 15, 21, 28 Dec)
### JavaScript
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

## 29 Nov 2020 (30, 01, 02, 04, 06, 09, 11, 18, 24, 31 Dec)