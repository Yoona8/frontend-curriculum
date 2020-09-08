# JavaScript

## ECMAScript Standard
<details>
<summary>Notes</summary>

Global changes:
- new strategy of spec updating
- new opportunities
  - template strings
  - function default params
  - arrow functions
  - destructuring
- better objects

</details>

## Code style
<details>
<summary>Tips</summary>

- Semi-colons `;` are placed after every expression except blocks of code `{}` (exceptions are objects and everything declared with `var`, `let` or `const`, basically variables)

</details>

## Constants and variables
<details>
<summary>General info</summary>

- `name = 'Mary';` works (JS adds `var name = Mary;`) but bad practice (not allowed with `'use strict';`)
- `var`
  - hoisting
  - `var i = 21; var i = 45;` recreating 
  - function and global scope (but no block scope)
  - `var undefined = 67;` reserved names usage (not allowed with `'use strict;`)
- `let`, `const` - no hoisting, no recreating, block scope, using reserved names is not allowed

</details>

<details>
<summary>Declarations (naming conventions)</summary>

- immutable (code agreement: protected, hardcoded) constant primitive value (physical constants, coefficients, etc)
```JavaScript
const LIGHT_SPEED = 255792458;
```
- immutable constant array
```JavaScript
const DEFAULT_NAMES = ['Michael', 'Anna', 'Chris'];
```
- immutable constant object (ex default configurations)
- enumeration
```JavaScript
const Earth = {
  RADIUS: 6.371,
  GRAVITATION: 6.67408
};

// consts
// not any const = constant
// declares a variable with immutable link
const element = document.querySelector('p');
const arr = [1, 2, 3, 4];
```

</details>

## Data types and structures
<details>
<summary>Table</summary>

|Name|Notes and usage|Level|
|----|---------------|:---:|
|undefined|`'undefined'`|:deciduous_tree:|
|Boolean|`'boolean'`|:blossom:|
|Number|`'number'`|:blossom:|
|String|`'string'`|:deciduous_tree:|
|BigInt|`'bigint'`|:seedling:|
|Symbol|`'symbol'`|:seedling:|
|null|`'object'`|:deciduous_tree:|
|Object|- `'object'`<br> - `Object`<br>- iterable lists: `Array`, collections<br>- collections: `NodeList`, `HTMLElementsList`, `classList`, `arguments`<br>- iterable dictionaries: `Map`, `WeakMap`<br>- iterable sets: `Set`, `WeakSet`|:deciduous_tree:|
|Function|`'function'`|:blossom:|

</details>

## Numbers

## Strings
<details>
<summary>How to remove duplicates?</summary>

- easy way is to convert into an array and use `Set`

</details>

## Iterables: Arrays
<details>
<summary>Creation</summary>

```JavaScript
// before ES6
var numbers = new Array();
var letters = [];

// ES6+
// make an array of any iterable (collection, separate values)
const elements = Array.from(document.querySelectorAll('li'));
const values = Array.of(1, 2, 3);
const items = [...elements, ...values];
```

</details>

<details>
<summary>Methods</summary>

|Method|Notes|Level|
|------|-----|:---:|
|`arr.sort()`|changes the initial array|:deciduous_tree:|
|`arr.splice()`|changes the initial array|:deciduous_tree:|
|`arr.filter()`|creates a new array|:deciduous_tree:|
|`arr.slice()`|creates a new array|:deciduous_tree:|
|`arr.map()`|creates a new array|:deciduous_tree:|
|`arr.reduce()`|creates a new value|:deciduous_tree:|

</details>

<details>
<summary>Arrays as a stack LIFO</summary>

- for tasks, when we have to store previous item (history, browser history, games)
- store the action (function) and add to the history array
- use `history.pop()();` to get back the stored value
- also available to 'go forward' the history (have to store the removed action back to the stack)

```JavaScript
history.push(() => {
  questions[0].text = oldText;
  return newText;
});
```

</details>

<details>
<summary>Arrays as a queue FIFO</summary>

- for tasks to be executed in a row after some async event
- for unique actions can use `Set` instead of `Array`

```JavaScript
const startAsync = () => {
  setTimeout(() => {
    for (const cb of callbacks) {
      callbacks.delete(cb);
      cb();
    }
  }, 500);
};

// before .find was used to check
// breaks the loop when the 1st item is found
callbacks.find((it) => it === 'some');
```

</details>

## Objects
<details>
<summary>Dictionaries</summary>

Object
- keys are strings or numbers (other not possible)
- not iterable (can use `for ... in` old cycle has some issues, not `for ... of`)
Map + WeakMap
- any keys possible
- iterable
- pairs are objects

```JavaScript
// object
const filterValueToScale = {
  'smallest': 0.25,
  'small': 0.5,
  'normal': 1,
  'large': 2
};

// map
let pairs = new Map();
pairs.set('John', 'May');
pairs.set('Ichigo', 'Rukiya');
// or with iterable
let pairs = new Map([['John', 'May'], ['Ichigo', 'Rukiya']]);
// iterating
for (const [first, second] of pairs) {
  console.log(first.name + second.name);
}
```

```JavaScript
// new features for objects in ES6
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
// destructuring
const newAntagonist = {...antagonist};
// new syntax for methods
const character = {
  _level: 1,
  // before
  go: function() {},
  // ES6
  go() {},
  // getters and setters
  // can't use getter/setter + property
  // can't address itself = infinite cycle
  get level() {
    return this._level;
  },
  // always strictly 1 parameter
  set level(value) {
    this._level = value;
  }
};
// addressing the getter or setter
const level = character.level;
character.level = 100;
// it there is only setter, can't access the value
```

</details>

<details>
<summary>Iterating</summary>

```JavaScript
// before ES6
// for ... in
// deprecated
// requires additional check, otherwise can go through the whole prototype chain

// ES6
// for ... of works
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
<summary>Delete a property or method</summary>

- `delete player.name;`

</details>

<details>
<summary>Check if property exists</summary>

```JavaScript
// but if the property = undefined, also returns false
player.name !== undefined;
// true even with undefined
'name' in player;
// true even if undefined
player.hasOwnProperty('name');
```

</details>

<details>
<summary>Copy</summary>

```JavaScript
// не избавляет от проблем с вложенностью
// {} - where
// player - what
const newPlayer = Object.assign({}, player);
// for several
const newPlayer = Object.assign({}, player, {options: 'code'});

// также не избавляет от проблем с вложенностью
const newPlayer = {...player};

// копирование с вложенностью - рекурсивно по всем ключам
// с проверкой typeof function or object
// есть в lodash
// hack with json.parse, json.stringify
```

</details>

## Functions
<details>
<summary>General info</summary>

- function without `return` statement returns `undefined`

</details>

<details>
<summary>Parameters vs Arguments</summary>

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
<summary>Anonymous function</summary>

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
<summary>Default parameters</summary>

```JavaScript
// Earlier
var doSomething = function (caption, amount, isChecked) {
  if (typeof isChecked === 'undefined') {
    isChecked = false;
  }
};

// ES2015
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
<summary>Arrow functions</summary>

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
<summary>Arguments keyword</summary>

- don't have to pass as a parameter (accessible as a keyword inside any function)
- iterable structure

</details>

<details>
<summary>Bind, call, apply</summary>

- `call` and `apply` call the function (as `()`)
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
<summary>Learn more</summary>

- [Functions on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)
- [Bind on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind)

</details>

## Scope
<details>
<summary>Notes</summary>

- scope where the function runs
- `this` links to current object in a `class`
- depends on how the function is called
- could be changed, also with `apply`, `call`, `bind`
- `bind` creates a new function, the initial function stays the same
- `bind` context can't be changed even with `apply`, `call`
- arrow functions do not have their context
- while the function is not called, it doesn't have any context
- context is being created upon the function call
- `this` assigns only upon the function call
- `use strict` affects `this` value
  - no `use strict` = `window`, with = `undefined`
- in an object (method) `this` = link to the object itself
- doesn't matter how the function is created, matters only how it's called
```JavaScript
const walk = function() {
  console.log(this + 'walk!');
};
const player = {walk};
player.walk(); // this === link to player object
walk(); // TypeError: Cannot read property '...' of undefined
```
- doesn't matter how the function is written, context will be the same `walk = player.walk`
- with closure the result is more obvious
```JavaScript
const guitarPlayer = {
  firstName: 'Michael',
  lastName: 'Lantsov',
  play() {
    console.log(`${guitarPlayer.firstName} ${guitarPlayer.lastName}`);
  }
};

// the result will be the same
const anotherPlayer = {
  play: guitarPlayer.play
};
```
- calling a function with binded context (1st param in those functions is always context, the 2nd parameter differs)
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
- listener's context is always === the element, to which the listener is applied `document.body` or `evt.currentTarget`
  - can override if create the event handler and execute the method
  ```JavaScript
  item.addEventListener('click', function() {
    cart.print();
  });
  // browser will store the function
  callback = cart.print;
  // and executes the callback
  callback();
  // so just won't work
  ```
- with bind (but careful, `bind` returns a new function, store first in a separate variable to unsubscribe if needed)
```JavaScript
item.addEventListener('click', cart.print.bind(cart));
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

if obj.getThis4 = obj.getThis2.bind(obj); then here obj.getThis4.call(a); we get this === obj instead of a (respects the first binding)
if created like that, always returns undefined (arrow functions have never their own this, only lexical scope's this, even if we use call or bind)
const obj = {
    getThis: () => this;
};
if we use new keyword to create an instance, lexical this will be the object (binds this in the constructor)
- [What is `this`? The Inner Workings of JavaScript Objects](https://medium.com/javascript-scene/what-is-this-the-inner-workings-of-javascript-objects-d397bfa0708a)

## Constructors and prototypes
<details>
<summary>Notes</summary>

- naming `GuitarPlayer`
- creation of an instance with new
- add a method in prototype
```JavaScript
GuitarPlayer.prototype.play = function() {};
```
- without new => undefined (void = return undefined) will not be created
- ES6 проверка if new inside constructor
```JavaScript
if (!new.target) { throw new Error(); }
```
- проверить принадлежность `instanceof`
- why new if we can return an object?
  - `instanceof` becomes useless
  - inheritance (prototype) won't work
- `new` keyword не вызывает функцию, а берет и на основе полей этой функции (то, что записывается через `this.name = name`) создает объект
  - созданный с `new GuitarPlayer` объект JS наделяет свойством вновь созданный объект, которое содержит информацию, с помощью какой функции-конструктора он создан
- если попробовать сымитировать функцию-конструктор и `return this;`, будет ссылаться на глобальный объект

</details>

## Classes
<details>
<summary>Notes</summary>

- `class Player {}` better to use instead of `const Singer = class {};`
- `constructor() {}` предопределенный метод класса, помогает создать экземпляр класса, все свойства определяются в нем
- `play() {}` методы записываются в `prototype`, определяются как у объекта
- `constructor` необязателен
- `new` для создания instance (or type error)
- если внутри класса обратиться к несуществующему свойству, получим `undefined`
- есть статические методы (не передаются потомкам (экземплярам))
```JavaScript
static createJuniorPlayer() {
  return new this(5, 2);
}
```
- также статическими могут быть свойства (но плохая поддержка)
- можно использовать getters / setters
- можно и без setter, но нарушим правило ООП, так как проверки будут снаружи
- приватные поля, но пока плохая поддержка `this.#skill = value;`

</details>

<details>
<summary>Difference between class and constructor functions</summary>

- `class` нельзя без `new` (в функции-конструкторе можно сделать имитацию с проверкой `target.new`)
- вывод в консоль (`class` / `f`)
- методы класса не перечисляемые
```JavaScript
for (const prop in player) {
  console.log(prop);
}
```

</details>

## Expressions, Control structures and Operators
<details>
<summary>Basic operators</summary>

- `=`
- `+` or `+=`
- `-` or `-=`
- `*` or `*=`
- `/` or `/=`
- `%`
- `**` exponentiation operator (not supported in IE)

</details>

<details>
<summary>Increment and decrement</summary>

- `return result++;` returns first the result and then increments
- `return --result;` decrements and then returns the changed value

</details>

<details>
<summary>Conditions and boolean operators</summary>

- `if ... else`
  - returns no value
- `? :`
  - always returns a value
- `switch () { case: ... }`
  - always uses `===` to compare
- falsy values
  - `0`
  - `''`
  - `NaN`
  - `null`
  - `undefined`
- truthy values
  - numbers `!== 0`
  - not empty strings
  - `[]`, `{}` and all other objects and arrays

<hr>

- `==` and `===`
- `!=` and `!==`
- `>` and `<`
```JavaScript
// JS compares strings based on standard lexicographical ordering (Unicode)
console.log('b' > 'a'); // => true

// JS always looks at the first char and only considers other chars if the 1st
// chars are the same
console.log('ab' > 'aa'); // => true

// uppercase chars are smaller than lowercase
console.log('a' > 'B'); // => true
```
- `>=` and `<=`
- `!`
  - `!!userName` converts into a boolean

<hr>

- `a && b` if both are true `=== true`
```JavaScript

// use value if the condition is true
const isLoggedIn = true; // if false => false
const userName = isLoggedIn && 'Mary'; // => 'Mary'

// returns the 1st falsy value
const useName = null && 'Mary'; // => null

// if both truthy, the second is returned
const userName = 'Max' && 'Mary'; // => 'Mary'

```
- `a || b` if at least one is true `=== true`
```JavaScript
// default value assignment
// doesn't convert into a boolean
// returns 1st truthy value
const userName = '' || 'Mary'; // => 'Mary'
const userName = 'Max' || 'Mary'; // => 'Max'

// if both falsy, the second value is returned
const userName = null || ''; // => ''
```
- `&&` precedence is higher than `||`

<hr>

- `isNaN()` to check if NaN or not

<hr>

- `isNaN(value) || value <= 0` if the first part is `true`, JS doesn't go further

</details>

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

<details>
<summary>Loops</summary>

- `for (let i = 0; i < 5; i++) {}`
- `for (const item of items) {}`
  - almost the same as `for` loop
  - can use `break` and `continue`
  - could be used with every iterable (not only `Array`)
- `for (const key in someObject) {}`
  - requires additional check, otherwise can go through the whole prototype chain
- `while (isEdit) {}` as long as the condition is true
- `do { ... } while (isEdit);` runs at least once

<hr>

- `break;` stops the loop execution
  - if inside the nested loop - stops only the nested one, outer continues
- `continue;` skips only the current iteration and moves to the next

<hr>

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
<summary>Rest and spread operators</summary>

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
<summary>New and instance of</summary>

- утиная типизация - ненадежно
- add some field to function, which will create an object and compare that key - велосипед
- функции-конструкторы
- more information [constructors and prototypes](#constructors-and-prototypes)

</details>

<details>
<summary>Try catch finally</summary>

- `throw { message: 'some message' };` can throw anything as an error, not only `new Error()`
- use `try {} catch (error) {}` only for the code you can't control (ex: server errors, user input)
- `try ... catch` or `try ... finally` but never `catch ... finally`
- if `try` doesn't throw an error, `catch` won't be executed
- why `finally`?
  - when we want to throw the error from inside the `catch` block to send to some statistics etc
  - some cleanup work (release data, clear the variables, etc)
- if the error is thrown from `catch`, only finally executes, code after `try ... catch ... finally` block won't be executed
- `finally` always runs

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

</details>

## 14 - Modules
<details>
<summary>Tasks to solve</summary>

- Namespace
  - no global scope
  - encapsulation
- Dependencies
  - easy to follow on what modules depends on
- Interface
  - methods and props export, easy to navigate

</details>

<details>
<summary>Before ES6</summary>

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
<summary>ES6 exports and imports</summary>

- `'use strict;'` by default
- syntax looks like destructuring, but not the same
- imported variable is not created, the same as in export
- better export const or class
- import without variable when just need to execute the code
- do not fold `export` and `import` into code blocks `{}`
- no hoisting, so that's why `import` is always on top
- `import` of unexcited variable = error, module won't be loaded
- there are dynamic imports, but browser support is still pretty low

Import paths:
- both `''` and `""` available
- path is a immutable constant, can't generate the path
- if 2 same imports => browser downloads only one
- paths abs or rel
  - `https://google.com` url
  - `/utils/helpers.js` abs domain-name
  - `./helpers.js` rel
  - `../helpers.js` rel
- `helpers.js` or `utils/helpers.js` is not supported (reserved for libs from package managers)
- If there is an error while downloading the module or its children => all connected modules won't be loaded

Modules loaders ()
- browsers: ES modules in browsers
- static: webpack, rollupJS, parcel, ...
- orders files
- downloads, stores files
- builds, minifies, packs

```JavaScript
// named
// names should be equal or error, module won't get loaded
// could import not all the export
// can't export the same variable 2x
// better not to combine line and group exports
export { name, age };
export const name = 'Max';
import { name } from './module-name.js';
// import all as child (ignores default, insecure, have no control on import)
import * as child from './module-name.js';

// renamed
export { name as userName};
import { name as userName} from './module-name.js';

// default
// better for classes
// could be hard to debug (imported by any name)
export default name;
export default { name };
export { name as default };
import name from './module-name.js';
```

```JavaScript
// proxy
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

- all dependencies load relatively to the 1st loaded module
- browser cashes not only a file, but also the result of executing the module + returned values

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

</details>

## 15 - DOM
<details>
<summary>Notes</summary>

- browser searches DOM in depths, so that the first tag is being found (otherwise not obvious)
- `querySelectorAll` `NodeList` static collection, DOM changes doesn't affect (nodes, not only DOM elements, also text, spaces, etc)
- `parentElement.children` `HTMLCollection` all those collections are live (only DOM elements)
- `getElementById` could be called only on `document`, not on element
- `appendChild` removes the element from where it was and adds to the new place (need to clone not to be removed)
- `element.cloneNode(boolean);` better to pass an argument (default could be different for some browsers)

</details>

<details>
<summary>Working with styles in JS</summary>

- `style` to get styles but only the inline styles
- `window.getComputedStyle` to get all styles applied to the element

</details>

<details>
<summary>Show password case</summary>

- change type of input from `password` to `text`

</details>

## 16 - Events
<details>
<summary>Events</summary>

- difference between `change` and `input`
  - `change` works when `field.value` changed and the user finished to enter the value (moved the handle and released)
  - `input` works with every value change

</details>

## 17 - Async JavaScript (promises and callbacks, async/await), http requests
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
  
<details>
<summary>Async ES5 (callbacks)</summary>

- async - run the operation without blocking the main script process
- minuses:
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
<summary>Async ES6 (promises)</summary>

- promise is a way to work with an async function as if it's sync
- returns an object, which replaces returned value, which is still undefined when the function already executed
- different states if a promise object
<img src="../images/promise.jpg" alt="promises" width="400">

```JavaScript
const getResponse = (url) => new Promise(
  (resolve, reject) => {
    // Object => Pending...
    const xhr = new XMLHttpRequest();
    xhr.open('GET', url);
    xhr.onload = () => resolve(xhr.response); // Object => Fulfilled
    xhr.onerror = () => reject(xhr.status); // Object => Rejected
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
  .catch((error) => console.warning(error));

// you can work with promises chaining then
// every then returns a promise, where we can also call then
Promise.resolve('a') // 'a'
  .then((val) => val.concat('b')) // 'ab'
  .then((val) => val.concat('c')) // 'abc'
  .then((val) => val.concat('d')); // 'abcd'
```

</details>

<details>
<summary>Async Promise.all</summary>

- when you need an array of requests at the same time (accepts an array of promises, runs at the same time, then calls when all the promises are resolved)
- `Promise.then` could return
  - just value/array - goes to the next promise
  - object Promise
  - array of values / promises - can turn into something else

</details>

<details>
<summary>Async fetch</summary>

- `fetch` is a wrapper above promise
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
```

</details>

<details>
<summary>Http</summary>

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
<summary>Feedback in UI</summary>

- When you sync data with a server, don't change control state, change only if the request was successful (returned 200+ codes)
- View => Model => Server => Model => View

Issues
- click on favorites - gone on update, if there was an error response from server
- comment doubles if you don't disable the submit button

</details>

## 17 - Authorization
<details>
<summary>Notes</summary>

- restricts the access for different users

</details>

<details>
<summary>Ways to identify a user</summary>

- Identification - tell the site who you are
- Authentication - (authentic - true, genuine) the confirmation that you are who you state you are
- Authorization - check if you are allowed to get access to some parts of the website or webapp

</details>

<details>
<summary>Authorization order</summary>

1. Identification - user enters login and password
2. Authentication - server checks if the login and password are correct and gives a token (access to the web app, often holds the rules and never stores open)
3. Authorization - you give the token to the server and the server decides whether to give you an access or not
  - 200 - success, allowed
  - 401 - unauthorized
  - 403 - not enough rights

</details>

## 18 - Working with data
<details>
<summary>Issues</summary>

- user input - user can enter unsafe data for the view and UI has to be ready for it
- storing and passing data formats could be different to the format needed on the UI, so we need to convert data in our app
  - some ES6 objects (Date, Sets, Maps) could not be converted to JSON, so have to convert into standard data types (primitives, arrays, objects)

</details>

## 19 - Browser storage

## 20 - Meta-programming

## 21 - Performance and optimizations
<details>
<summary>Code parsing, compilation and execution</summary>

<img src="../images/code-parsing.png" alt="Code parsing">

<img src="../images/heap-stack.png" alt="Heap, stack (how JS engine works)">

- JS is single-threaded
- event loop is not a JS-engine feature (only heap and stack - simple sync code), it's a browser feature

</details>

<details>
<summary>Primitive and Reference values</summary>

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
<summary>Garbage collection and Memory management</summary>

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

## 22 - Security

## 23 - Regular expressions
<details>
<summary>Notes</summary>

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

## 23 - Deploying

## 24 - Testing

## 25 - Debugging
<details>
<summary>Learn more</summary>

- [Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/)

</details>

## 26 - Browser support

## 27 - Tools and workflow

## 28 - Libraries

## 29 - Frameworks

## Notes
<details>
<summary>Other</summary>

- cycle is more optimal than a recursion (call stack overflow), any recursion could be rewritten into a cycle
- you can also use `element.textContent++;` instead of `element.textContent = element.textContent++;
- `parent.append(child);` removes child and moves to the new place (if existed)
- `data-cat-name="Cat"` access from JS `element.dataset.catName`

</details>