# Review progress and questions I have to review
## 17, ..., 17 Dec 2020 (24 Dec)
### JavaScript
<details>
<summary>What is a scope and a context?</summary>

- scope is where the function runs
- context depends on how the function is called
- while the function is not called, it doesn't have any context
- context is being created upon the function call

</details>

## 24, ..., 20 Dec 2020 (27 Dec)
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

## 26, ..., 23 Dec 2020 (30 Dec)
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

## 29, ..., 20 Dec 2020 (26, 02 Jan)
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

## 02, ..., 17 Dec 2020 (24, 30, 06 Jan)
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

## 10, ..., 22 Dec 2020 (29, 04, 11 Jan)
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

## 14, ..., 22 Dec 2020 (26, 01, 08, 15 Jan)
### JavaScript
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

## 16, ..., 21 Dec 2020 (24, 28, 03, 10, 17 Jan)
### JavaScript
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

## 18, ..., 21 Dec 2020 (23, 26, 30, 05, 12, 19 Jan)
### JavaScript
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

## 19, ..., 22 Dec 2020 (24, 27, 31, 06, 13, 20 Jan)
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

## 23 Dec 2020 (24, 25, 26, 28, 31, 04, 10, 17, 24 Jan)