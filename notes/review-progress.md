# Review progress and questions I have to review
## 10, ..., 08 Dec 2020 (15 Dec)
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

## 12, ..., 13 Dec 2020 (20 Dec)
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

## 13, ..., 13 Dec 2020 (20 Dec)
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

## 16, ..., 09 Dec 2020 (15, 22 Dec)
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

## 17, ..., 11 Dec 2020 (17, 24 Dec)
### JavaScript
<details>
<summary>What is a scope and a context?</summary>

- scope is where the function runs
- context depends on how the function is called
- while the function is not called, it doesn't have any context
- context is being created upon the function call

</details>

## 24, ..., 07 Dec 2020 (14, 20, 27 Dec)
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

## 26, ..., 10 Dec 2020 (17, 23, 30 Dec)
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

## 29, ..., 13 Dec 2020 (20, 26, 02 Jan)
### JavaScript
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

## 02, ..., 12 Dec 2020 (15, 17, 24, 30, 06 Jan)
### JavaScript
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

## 10, ..., 13 Dec 2020 (15, 17, 20, 22, 29, 04, 11 Jan)
### JavaScript
<details>
<summary>What are the basic math operators?</summary>

- `=`
- `+` or `+=`
- `-` or `-=`
- `*` or `*=`
- `/` or `/=`
- `%`
- `**` exponentiation operator (not supported in IE)

</details>

<details>
<summary>What is the difference between postfix and prefix increment and decrement?</summary>

- `return result++;` returns first the result and then increments
- `return --result;` decrements and then returns the changed value

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
switch (expression) {
  case value: 
    console.log(value);
    break;
  default:
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
- not empty strings
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
<summary>What is `not` operator and how to convert into boolean?</summary>

- `!`
- `!!userName` converts into a boolean

</details>

<details>
<summary>What are boolean operators and which one is higher?</summary>

- `a && b` if both are true `=== true`
```JavaScript
// use value if the condition is true
const isLoggedIn = true; // if false => false
const userName0 = isLoggedIn && 'Mary'; // => 'Mary'

// returns the 1st falsy value
const userName1 = null && 'Mary'; // => null

// if both truthy, the second is returned
const userName2 = 'Max' && 'Mary'; // => 'Mary'
```
- `a || b` if at least one is true `=== true`
```JavaScript
// default value assignment
// doesn't convert into a boolean
// returns 1st truthy value
const userName1 = '' || 'Mary'; // => 'Mary'
const userName2 = 'Max' || 'Mary'; // => 'Max'

// if both falsy, the second value is returned
const userName3 = null || ''; // => ''
```
- `&&` precedence is higher than `||`

</details>

<details>
<summary>How to check if the value is `NaN`?</summary>

- `isNaN()` to check if NaN or not
- `isNaN(value) || value <= 0` if the first part is `true`, JS doesn't go further

</details>

## 14 Dec 2020 (15, 16, 17, 19, 22, 26, 01, 08, 15 Jan)
